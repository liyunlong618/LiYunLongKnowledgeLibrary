

___________________________________________________________________________________________
###### [GoMenu](../UE_Effect_Menu.md)
___________________________________________________________________________________________
# 003_3Dmax帧数区间动画导出、定序器、激活特效关键帧


___________________________________________________________________________________________


## 目录

[TOC]


------

## 3Dmax导入导出动画，选择动画帧数区间导出

> 86~197
>
> ![image-20250317181523907](./Image/UE_EffectBaseV003/image-20250317181523907.png)![image-20250317181903169](./Image/UE_EffectBaseV003/image-20250317181903169.png)![image-20250317182004919](./Image/UE_EffectBaseV003/image-20250317182004919.png)![image-20250317182306958](./Image/UE_EffectBaseV003/image-20250317182306958.png)
>
> ### 导出为FBX

------

## 区间动画FBX导入UE

### 如果导入的模型比较小可以设置导入时缩放

> ![image-20250317182623061](./Image/UE_EffectBaseV003/image-20250317182623061.png)![image-20250317182542665](./Image/UE_EffectBaseV003/image-20250317182542665.png)

### 如果有部分材质看不到可能是系统识别为透明材质

> ![image-20250317184023539](./Image/UE_EffectBaseV003/image-20250317184023539.png)

### 需要看下材质贴图有无Alpha，如果有可以使用Mask模式

> ![image-20250317220251394](./Image/UE_EffectBaseV003/image-20250317220251394.png)![image-20250317220330682](./Image/UE_EffectBaseV003/image-20250317220330682.png)

### 双面材质

> ![image-20250317220427770](./Image/UE_EffectBaseV003/image-20250317220427770.png)

------

## 使用定序器

### 1.创建关卡序列

> ![image-20250317220810713](./Image/UE_EffectBaseV003/image-20250317220810713.png)![image-20250317221344029](./Image/UE_EffectBaseV003/image-20250317221344029.png)

### 需要注意！关卡序列与当前关卡绑定!!!

> ![image-20250318002630337](./Image/UE_EffectBaseV003/image-20250318002630337.png)

### 2.添加角色和动画到关卡序列

> ![image-20250317221541513](./Image/UE_EffectBaseV003/image-20250317221541513.png)![image-20250317221652684](./Image/UE_EffectBaseV003/image-20250317221652684.png)

### 3.添加法阵粒子到关卡序列

> ![image-20250317222114824](./Image/UE_EffectBaseV003/image-20250317222114824.png)

#### 添加激活关键帧

##### 使用`Trigger`触发

> ![image-20250317223155017](./Image/UE_EffectBaseV003/image-20250317223155017.png)![image-20250317223825328](./Image/UE_EffectBaseV003/image-20250317223825328.png)

##### 使用`Activate`和`Deactivate`开启和关闭，必须两个配合使用！！！

> Trigger和`Activate`、`Deactivate`的区别有点像动画通知和动画状态通知的区别
>
> 一个是一次性触发，一个是持续状态![image-20250317224429253](./Image/UE_EffectBaseV003/image-20250317224429253.png)

------

## 再制作一个法阵

> ![image-20250317234850083](./Image/UE_EffectBaseV003/image-20250317234850083.png)![image-20250317234910215](./Image/UE_EffectBaseV003/image-20250317234910215.png)

------
