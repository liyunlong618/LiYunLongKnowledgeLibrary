

___________________________________________________________________________________________
###### [GoMenu](../UE_Effect_Menu.md)
___________________________________________________________________________________________
# 002_粒子系统简介、法阵制作


___________________________________________________________________________________________


## 目录

[TOC]


------

## 相关文件夹结构创建

> 创建文件夹，选择位置，命名并保存
>
> ![image-20250311021507164](./Image/UE_EffectBaseV002/image-20250311021507164.png)

------

## 导入贴图

> 百度云：
>
> ```
> https://pan.baidu.com/s/1F3JUtwbBtfOAvtuq0MGhHg?pwd=an5f
> ```
>
> ![image-20250311021312337](./Image/UE_EffectBaseV002/image-20250311021312337.png)

------

## 粒子系统界面介绍

### 开启;隐藏;独显

> ![image-20250316104418864](./Image/UE_EffectBaseV002/image-20250316104418864.png)![image-20250316104609470](./Image/UE_EffectBaseV002/image-20250316104609470.png)

### 重新播放

> ![image-20250316112936459](./Image/UE_EffectBaseV002/image-20250316112936459.png)

------

### 粒子预览窗口有些虚（调整设置）

> #### 设置为`FXAA(快速抗锯齿)`
>
> ![image-20250316114746926](./Image/UE_EffectBaseV002/image-20250316114746926.png)

------

### 粒子默认方向为朝向摄像机，修改为垂直向上（打平）

> ![image-20250316115111221](./Image/UE_EffectBaseV002/image-20250316115111221.png)![image-20250316115651560](./Image/UE_EffectBaseV002/image-20250316115651560.png)![image-20250316115750810](./Image/UE_EffectBaseV002/image-20250316115750810.png)

------

## 粒子的发射方式

### 持续发射

> ![image-20250316105358881](./Image/UE_EffectBaseV002/image-20250316105358881.png)![image-20250316105710326](./Image/UE_EffectBaseV002/image-20250316105710326.png)![image-20250316110514641](./Image/UE_EffectBaseV002/image-20250316110514641.png)

### 爆发模式

> ![image-20250316111215365](./Image/UE_EffectBaseV002/image-20250316111215365.png)

### 需要注意！当爆炸时间小于粒子持续时间时,不会生成粒子!!!!
> ![image-20250316113241726](./Image/UE_EffectBaseV002/image-20250316113241726.png)

------

## 设置粒子初始大小，使用`正方形模式`和`长方形模式`

#### 默认为正方形模式

- 即X和Y和Z相等，且取最大值，比如（25，0，0）读取为（25，25，25）<img src="./Image/UE_EffectBaseV002/image-20250316121521232.png" alt="image-20250316121521232" style="zoom:50%;" />

> ![image-20250316120642963](./Image/UE_EffectBaseV002/image-20250316120642963.png)![image-20250316120738072](./Image/UE_EffectBaseV002/image-20250316120738072.png)![image-20250316121049413](./Image/UE_EffectBaseV002/image-20250316121049413.png)

#### 长方形模式（长宽高不等）

<img src="./Image/UE_EffectBaseV002/image-20250316121436782.png" alt="image-20250316121436782" style="zoom:50%;" />

> 再调整就可以生效了![image-20250316121646697](./Image/UE_EffectBaseV002/image-20250316121646697.png)

------

## 调整颜色渐变和Alpha的原理

> ![image-20250316124008754](./Image/UE_EffectBaseV002/image-20250316124008754.png)

### 调整亮度（发光强度）

> 因为在材质里使用了自发光，所以可以调整亮度 `H` `S` `V`的`V`大于`1.f`，如下图：会出现特别亮的光晕
>
> ![image-20250316124423838](./Image/UE_EffectBaseV002/image-20250316124423838.png)

### 添加关键帧

> 添加关键帧，添加之后需要根据Index顺序设置参数（需要从`0`到`1`的过程）
>
> ![image-20250317170248537](./Image/UE_EffectBaseV002/image-20250317170248537.png)![image-20250317170609865](./Image/UE_EffectBaseV002/image-20250317170609865.png)

### 查看曲线，按住`Ctrl+Alt`可以框选点

> ![image-20250317170826442](./Image/UE_EffectBaseV002/image-20250317170826442.png)![image-20250317171019625](./Image/UE_EffectBaseV002/image-20250317171019625.png)![image-20250317171143384](./Image/UE_EffectBaseV002/image-20250317171143384.png)![image-20250317171219825](./Image/UE_EffectBaseV002/image-20250317171219825.png)

------

## 设置初始旋转和旋转速率

> <img src="./Image/UE_EffectBaseV002/image-20250317171915705.png" alt="image-20250317171915705" style="zoom: 67%;" /><img src="./Image/UE_EffectBaseV002/image-20250317172153666.png" alt="image-20250317172153666" style="zoom: 67%;" />![image-20250317172648571](./Image/UE_EffectBaseV002/image-20250317172648571.png)

------

## 根据生命周期调整大小变化`SizeByLife`

> 首先初始大小在[InitialSize中](#设置粒子初始大小，使用`正方形模式`和`长方形模式`)调整，这里**只会调整百分比！！！！**
>
> ![image-20250317172840955](./Image/UE_EffectBaseV002/image-20250317172840955.png)![image-20250317173515843](./Image/UE_EffectBaseV002/image-20250317173515843.png)

------

## 创建法阵

### 1.使用UE4创建粒子系统

> ![image-20250315144551274](./Image/UE_EffectBaseV002/image-20250315144551274.png)

------

### 2.创建粒子要使用的材质球

> ![image-20250315145209368](./Image/UE_EffectBaseV002/image-20250315145209368.png)![image-20250315145403676](./Image/UE_EffectBaseV002/image-20250315145403676.png)

------

### 3.颜色属性的调整

> ![image-20250316103139742](./Image/UE_EffectBaseV002/image-20250316103139742.png)![image-20250316103430181](./Image/UE_EffectBaseV002/image-20250316103430181.png)![image-20250316103906964](./Image/UE_EffectBaseV002/image-20250316103906964.png)

------

### 4.粒子系统命名

> ![image-20250316104801745](./Image/UE_EffectBaseV002/image-20250316104801745.png)![image-20250316104950793](./Image/UE_EffectBaseV002/image-20250316104950793.png)

------

### 5.设置粒子参数

> 1. 不使用循环模式，改用爆发模式生成一次
>
> ![image-20250316114006799](./Image/UE_EffectBaseV002/image-20250316114006799.png)![image-20250316114145300](./Image/UE_EffectBaseV002/image-20250316114145300.png)

------

### 6.粒子默认方向为朝向摄像机，修改为垂直向上（打平）

> ![image-20250316115111221](./Image/UE_EffectBaseV002/image-20250316115111221.png)![image-20250316115651560](./Image/UE_EffectBaseV002/image-20250316115651560.png)![image-20250316115750810](./Image/UE_EffectBaseV002/image-20250316115750810.png)

------

### 7.设置粒子

#### （1）初始大小[使用默认的`正方形模式`就行点击这里跳转上面](#设置粒子初始大小使用`正方形模式`和`长方形模式`)

#### （2）颜色变化[参考上面的颜色设置渐变，点击这里跳转上面](#调整亮度（发光强度）)

#### （3）设置[初始随机旋转和旋转速率](#设置初始旋转和旋转速率)和[根据生命周期调整大小变化`SizeByLife`](#根据生命周期调整大小变化`SizeByLife`)

------

## GIF完成法阵部分

> ![11120250317_175031](./Image/UE_EffectBaseV002/11120250317_175031.gif)

------

> 下一节搞动画部分，从`3Dmax`中导入

------
