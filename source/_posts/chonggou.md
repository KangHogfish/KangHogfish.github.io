---
title: 重构-改善既有代码的设计：函数重构-重新组织函数的九种方法
date: '2024-01-19 01:11:24'
updated: '2024-01-28 21:51:15'
permalink: >-
  /post/reconstructionimproving-the-design-of-existing-code-function-reconstructionnine-methods-of-reorganizing-functions-onibn.html
comments: true
toc: true
---
# 重构-改善既有代码的设计：函数重构-重新组织函数的九种方法

一、函数逻辑相关

1. Extract Method 提炼函数：由复杂的函数提炼出独立的函数或者说大函数分解成由小函数组成

    ​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401281932383.png?token=BAOVSBBJK2BVOPZBS6V4METFWY5ZC)​
2. Inline Method 内联函数：直接使用函数体代替函数调用

    ​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401281932810.png?token=BAOVSBCCXQVFTPSHJPHGF6DFWY5Y4)​
3. Replace Method with Method object 函数对象取代函数：大函数变成类

    ​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401281932777.png?token=BAOVSBFRIXBJRR7DUAMSKALFWY5Y6)​

二、函数局部变量重构

4. Inline Temp 内联临时变量：表达式代替临时变量

    ​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401282142438.png?token=BAOVSBEZCOO4B5GQAPCMDFLFWZNAM)​

5. Replace Temp with Query 以查询函数代替临时变量：独立函数代替表达式

    ​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401281932555.png?token=BAOVSBA4TFTPPZQCHWCXYWLFWY5YU)​

    ​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401281932486.png?token=BAOVSBBAWOCFBJW3LCDEX53FWY5YW)​

6. Introduce Explaining Variable 引入解释性变量：复杂表达式分解为临时解释性变量

    ​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401281932126.png?token=BAOVSBCS4J2TEDJPLNGV4LTFWY5YW)​

7. Split Temporary Variable 分解临时变量：临时变量不应该被赋值超过一次

    ​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401281932954.png?token=BAOVSBFXGRDZMTCAYFF2ITDFWY5YY)​

三、函数参数重构和算法重构

8. Remove Assigments to Parameters 移除对参数的赋值：不要对参数赋值

    ​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401281932278.png?token=BAOVSBDRUFBJWX24WJ6DRI3FWY5YM)​

9. Substitute Algorithm 替换算法：函数本体替换为另一个算法

    ​![image](https://raw.githubusercontent.com/KangHogfish/PicBed/main/asset/202401281932255.png?token=BAOVSBDFROCMET7P2HZMCXDFWY5YO)​
