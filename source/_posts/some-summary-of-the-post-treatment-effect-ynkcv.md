---
title: 后处理效果的一些总结
date: '2024-01-09 01:25:22'
updated: '2024-01-30 01:42:10'
permalink: /post/some-summary-of-the-post-treatment-effect-ynkcv.html
comments: true
toc: true
---

# 后处理效果的一些总结

​​​​​​

所谓后处理（Post-processing)，是指在正常渲染管线结束后，对最终渲染图像进行的后期加工，如滤镜等。以此来模拟物理摄像机和电影特效。

下图是UE4和Unity中共有且比较常用的后处理效果思维导图：

​​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401300142715.png)​​

### <span style="font-weight: bold;" data-type="strong">抗锯齿 Anti-aliasing</span>

产生锯齿的根本原因是由于纹理采样频率与着色频率不同所致，也就是说，当我们的纹理尺寸与屏幕分辨率差距过大时，很容易出现锯齿现象。为了解决这一问题，就需要提高着色采样频率，最直观的方式就是SSAA，但是这么做会成倍地增加性能开销，所以一般前向渲染更多地是会用MSAA。但考虑到延迟渲染，MSAA并不友好，因此目前主流的抗锯齿技术应该是 <span style="font-weight: bold;" data-type="strong">快速近似抗锯齿(FXAA)</span>  和 <span style="font-weight: bold;" data-type="strong">时间性抗锯齿(TAA)</span>  。

### <span style="font-weight: bold;" data-type="strong">FXAA</span>

基于边缘检测的抗锯齿算法，但是容易产生边缘闪烁的现象。

​![](https://pic4.zhimg.com/80/v2-038aba941d13cf7db4b1e37d245d29bf_720w.webp)​

上图是英伟达给出的Anti-aliasing效果图，左侧是关闭抗锯齿，中间是4xMSAA，最右侧是3级FXAA。

### <span style="font-weight: bold;" data-type="strong">TAA</span>

把多次采样的过程分布到每一帧中去，也就是每一帧都利用前面几帧保存下来的数据。

​![](https://pic3.zhimg.com/80/v2-060ffe489d8bdadfc0229eeaebd85786_720w.webp)​

​![](https://pic3.zhimg.com/80/v2-c329f7e5c698b0fc28aa25a0447013fa_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">泛光 Bloom</span>

模拟了亮度较强区域周围的泛光效果，帮助给LDR图像增加真实感。

​![](https://pic2.zhimg.com/80/v2-97629d9d2bbeae22f68cf0ee476c0245_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">镜头耀斑 Lens Flares</span>

模拟了相机镜头在拍摄强光时产生的光斑，常与Bloom效果搭配使用。

​![](https://pic2.zhimg.com/80/v2-d247c12dfdbb116e76b3b6ae53834ed9_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">颜色分级 Color Grading</span>

俗称调色，是游戏后期处理中最常见也是必要的一个环节。它能够改变或矫正最终图像的颜色和亮度，类似滤镜的效果。

### <span style="font-weight: bold;" data-type="strong">白平衡 White Balance</span>

特定光源下出现的偏色现象，通过校准色温来进行补偿，得到想要的效果。

色温（Temp）值高于场景光线的时候，场景会呈现偏黄的暖色，相反则会呈现偏蓝的冷色。

色调（Tint）通过调节青色和洋红色范围来调整场景的白平衡温度色调，用于平衡所产生的颜色，让颜色看起来更自然一些。

### <span style="font-weight: bold;" data-type="strong">饱和度 Saturation</span>

色调的纯度，饱和度越高，看起来就越近原色（RGB）；饱和度降低，颜色的灰色或褪色效果更明显。

### <span style="font-weight: bold;" data-type="strong">对比度 Contrast</span>

调节场景中光线和深色值的色调范围，降低对比度会去除高亮，让图像显得更亮，营造出一种褪色的效果；加强对比度会增加高亮，让整体图像变暗。

### <span style="font-weight: bold;" data-type="strong">伽马校正 Gamma</span>

通过伽马函数调节图像中间色调的亮度以准确重现颜色。降低或增大该值会让图像呈现出褪色或过暗的效果。

### <span style="font-weight: bold;" data-type="strong">颜色增益 Gain</span>

调节图像白色（高亮）的亮度以准确重现颜色。增大或降低该值会让图像呈现出褪色或过暗的效果。

### <span style="font-weight: bold;" data-type="strong">颜色偏移 Offset</span>

调节图像黑色（阴影）的亮度以准确重现颜色。增大或降低该值会让图像阴影呈现出褪色或过暗的效果。

### <span style="font-weight: bold;" data-type="strong">色调映射 Tone Mapper</span>

将HDR颜色映射到LDR颜色空间。

美国电影艺术与科学学会发明了Academy Color Encoding System(AECS)，是一套颜色编码系统，或者说是一个新的颜色空间。它是一个通用的数据交换格式，一方面可以不同的输入设备转成ACES，另一方面可以把ACES在不同的显示设备上正确显示。

### <span style="font-weight: bold;" data-type="strong">景深 Depth of Field</span>

模拟摄像机聚焦前后的模糊效果，实现原理就是根据深度和设置将屏幕空间分为三层：近景、远景和聚焦层。其中，近景层和远景层总是模糊的，与非模糊的聚焦层相融合。

​![](https://pic1.zhimg.com/80/v2-804aad477d322254d5e3c22bbbf1bf68_720w.webp)​

如上图，绿色部分为近景层，蓝色部分为远景层，中间黑色包括角色的部分为聚焦层。该图实际渲染出来的效果如下：

​![](https://pic4.zhimg.com/80/v2-8449b7f37dbbe62620f2da88754cc623_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">环境光遮蔽 Ambient Occlusion</span>

一种近似计算因遮蔽而造成的光线衰减的效果。通常是在标准全局光照的基础上增添细微效果，例如让角落、裂缝或其他生物变暗，以形成一种更加自然真实的视觉效果。

​![](https://pic2.zhimg.com/80/v2-f3f9c125c5acb980cc08d079d83eeb55_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">运动模糊 Motion Blur</span>

运动模糊就是模拟摄像机在曝光时，场景发生变化而产生的模糊效果。常见的方法是利用一张速度缓存来存储屏幕各个像素当前的运动速度，然后利用该值来决定模糊的方向和大小。

​![](https://pic4.zhimg.com/80/v2-557882642f269334e042d5a698232a2b_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">图片效果 Image Effect</span>

### <span style="font-weight: bold;" data-type="strong">Chromatic Aberation</span>

模拟相机镜头产生的颜色偏移效果，效果如下：

​![](https://pic4.zhimg.com/80/v2-ad9aaeec083198e6b0d8ca1878be9e5b_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">Vignette</span>

模拟镜头边缘被遮挡导致的偏暗效果，效果如下：

​![](https://pic2.zhimg.com/80/v2-7703f6638d359a15389f24a3f9991ad1_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">Grain</span>

模拟老式相机拍出的颗粒感，效果如下：

​![](https://pic4.zhimg.com/80/v2-1b74a6e81ad5b6b15fc131ad123e43af_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">自动曝光 Auto Exposure</span>

当场景整体亮度偏暗或者偏亮时，会自动调节曝光度，使得场景不至于过亮或过暗，并保持场景中的细节，如模拟人眼在从明亮场景进入黑暗场景时的体验。

​![](https://pic4.zhimg.com/80/v2-39cc1ddc7eb50aaf414d9011c9c2b557_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">屏幕空间反射 Screen Space Reflection</span>

简称SSR，基于延迟渲染，针对屏幕空间下物体的每个像素，根据摄像机到该像素的摄像以及对应法线求出反射方向，再进行<span style="font-weight: bold;" data-type="strong">光线步进</span>计算，即沿着反射方向每走一个单位距离便判断下步进后的深度值与G-buffer中存储的深度值是否相等。如果相等表示出现了交点，求出物体交点处的颜色以作为反射颜色。

​![](https://pic3.zhimg.com/80/v2-71b6a6fe86f060a3db8f71076fa9fdd2_720w.webp)​

### <span style="font-weight: bold;" data-type="strong">自定义效果</span>

虚幻引擎中使用 <span style="font-weight: bold;" data-type="strong">Post Process Material</span> 来实现一些自定的后处理效果。与普通的材质蓝图相同，但需要将类型设置为“Post Process”，并且输出颜色只需用到 <span style="font-weight: bold;" data-type="strong">Emissive Color</span>。

在后处理材质中最常用的就是 SceneTexture ，可以根据不同的id来使用不同的功能。以一个最简单的后处理描边效果举例，根据SceneTexture的SceneDepth做上下左右四个方向的轻微偏移并做差，得到一个边缘，再与新的SceneTexture的PostProcessInput0相结合，得到一物体带描边的效果。

​![](https://pic1.zhimg.com/80/v2-addedf75834d5a366b9f37aa48562620_720w.webp)​

​![](https://pic2.zhimg.com/80/v2-6728d2036022f5a39632680b655ef1f5_720w.webp)​

‍
