___________________________________________________________________________________________
###### [GoMenu](../3DMaxBasicsMenu.md)
___________________________________________________________________________________________
# 008_AR场景建模、模型操作、模型减面


___________________________________________________________________________________________

## 目录

- [008\_AR场景建模](#008_ar场景建模)
  - [目录](#目录)
  - [步骤流程：](#步骤流程)
    - [1. 检查单位是否为  cm](#1-检查单位是否为--cm)
    - [2. 仔细观察原画](#2-仔细观察原画)
    - [4. 拆分部分，将大块拆分为基本几何体](#4-拆分部分将大块拆分为基本几何体)
    - [5. 外侧边缘发亮的部分，可以对线使用切角（使用切角后一定要处理点，容易出问题）](#5-外侧边缘发亮的部分可以对线使用切角使用切角后一定要处理点容易出问题)
    - [6. 对结构不产生影响的边要删掉！！！](#6-对结构不产生影响的边要删掉)
    - [7. 建完模型反复比对原画修改！！！](#7-建完模型反复比对原画修改)
  - [模型操作](#模型操作)
    - [锁边](#锁边)
    - [一条边分离成两条](#一条边分离成两条)
    - [从模型上提取线](#从模型上提取线)
    - [可以软选择调整的方法](#可以软选择调整的方法)
      - [1. FFD 2x2x2](#1-ffd-2x2x2)
      - [2. FFD 3x3x3](#2-ffd-3x3x3)
      - [可以选中部分点单独调整，不影响其他部分](#可以选中部分点单独调整不影响其他部分)
      - [3. 软选择](#3-软选择)
      - [启用软选择（角色建模中很常用）](#启用软选择角色建模中很常用)
    - [缓慢放大](#缓慢放大)
    - [添加文字](#添加文字)
      - [创建方式](#创建方式)
      - [使用形状渲染样条线](#使用形状渲染样条线)
      - [降低弧度（减少点）](#降低弧度减少点)
      - [填充文字](#填充文字)
      - [可以对边使用 挤出 + 倒角](#可以对边使用-挤出--倒角)
    - [创建半圆半方的几何体：](#创建半圆半方的几何体)
    - [使用螺旋线创建麻绳](#使用螺旋线创建麻绳)
      - [1. 创建螺旋线，使用渲染，沿样条线生成集合体](#1-创建螺旋线使用渲染沿样条线生成集合体)
      - [2. 然后转为可编辑多边形](#2-然后转为可编辑多边形)
      - [3. 然后使用修改器：路径变形(WSM)](#3-然后使用修改器路径变形wsm)
      - [4. 然后选择样条线，调整参数](#4-然后选择样条线调整参数)
      - [5. 完成后使用 "塌陷" 保存修改](#5-完成后使用-塌陷-保存修改)
    - [模型减面](#模型减面)
      - [也可以修改成隔两个选一个的](#也可以修改成隔两个选一个的)
    - [使用 "快速切线" 功能](#使用-快速切线-功能)
    - [镂空栅栏的类似做法](#镂空栅栏的类似做法)



------

## 步骤流程：

### 1. 检查单位是否为  cm

### 2. 仔细观察原画

- 观察各部位之间的比例

### 4. 拆分部分，将大块拆分为基本几何体

### 5. 外侧边缘发亮的部分，可以对线使用切角（使用切角后一定要处理点，容易出问题）

### 6. 对结构不产生影响的边要删掉！！！

### 7. 建完模型反复比对原画修改！！！

------

## 模型操作

### 锁边

> 可以将边锁住，防止调整边的位置影响形状和结构
>
> ![image-20250211150704069](./Image/3DMaxBaseV008/image-20250211150704069.png)

------

### 一条边分离成两条

> 想让下图的这个模型沿线分离成两个部分
>
> <img src="./Image/3DMaxBaseV008/image-20250211151123414.png" alt="image-20250211151123414" style="zoom:33%;" />
>
> ![image-20250211151348734](./Image/3DMaxBaseV008/image-20250211151348734.png)
>
> 再调整点或者边分开即可
>
> ![image-20250211151452013](./Image/3DMaxBaseV008/image-20250211151452013.png)

------

### 从模型上提取线

> 线模式下，选择线
>
> 尽可能使用线性，因为平滑是贝塞尔会多出来一堆的点
>
> ![image-20250211151851423](./Image/3DMaxBaseV008/image-20250211151851423.png)![image-20250211152135759](./Image/3DMaxBaseV008/image-20250211152135759.png)

------

### 可以软选择调整的方法

#### 1. FFD 2x2x2

#### 2. FFD 3x3x3

> <img src="./Image/3DMaxBaseV008/image-20250211153529851.png" alt="image-20250211153529851" style="zoom: 67%;" />

#### 可以选中部分点单独调整，不影响其他部分

> 比如：
>
> ![Screenshot_2025-02-11-16-12-09-657_com.baidu.netdisk-edit](./Image/3DMaxBaseV008/Screenshot_2025-02-11-16-12-09-657_com.baidu.netdisk-edit.jpg)

------

#### 3. 软选择

> 比如将一个正圆形的顶，调整为弧面
>
> ![123123](./Image/3DMaxBaseV008/123123.png)

#### 启用软选择（角色建模中很常用）

> ![image-20250211153345421](./Image/3DMaxBaseV008/image-20250211153345421.png)![image-20250211153401180](./Image/3DMaxBaseV008/image-20250211153401180.png)

------

### 缓慢放大

Ctrl+Alt+中键  拖动模型

- 用来微调，和参考图对比

### 添加文字

#### 创建方式

> ![image-20250211161901255](./Image/3DMaxBaseV008/image-20250211161901255.png)

#### 使用形状渲染样条线

> ![image-20250211161935288](./Image/3DMaxBaseV008/image-20250211161935288.png)

#### 降低弧度（减少点）

> ![image-20250211162104340](./Image/3DMaxBaseV008/image-20250211162104340.png)

#### 填充文字

> 直接转成多边形，就会被填充
>
> ![image-20250211162321797](./Image/3DMaxBaseV008/image-20250211162321797.png)

#### 可以对边使用 挤出 + 倒角

> ![image-20250211163148099](./Image/3DMaxBaseV008/image-20250211163148099.png)

------

### 创建半圆半方的几何体：

> ![Screenshot_2025-02-12-10-21-50-470_com.baidu.netdisk-edit](./Image/3DMaxBaseV008/Screenshot_2025-02-12-10-21-50-470_com.baidu.netdisk-edit.jpg)

------

### 使用螺旋线创建麻绳

#### 1. 创建螺旋线，使用渲染，沿样条线生成集合体

> ![image-20250212113210142](./Image/3DMaxBaseV008/image-20250212113210142.png)![image-20250212113453523](./Image/3DMaxBaseV008/image-20250212113453523.png)

#### 2. 然后转为可编辑多边形

#### 3. 然后使用修改器：路径变形(WSM)

> ![image-20250212122139914](./Image/3DMaxBaseV008/image-20250212122139914.png)![Screenshot_2025-02-12-12-14-16-220_com.baidu.netdisk-edit](./Image/3DMaxBaseV008/Screenshot_2025-02-12-12-14-16-220_com.baidu.netdisk-edit.jpg)

#### 4. 然后选择样条线，调整参数

> ![image-20250212122618494](./Image/3DMaxBaseV008/image-20250212122618494.png)![image-20250212122635668](./Image/3DMaxBaseV008/image-20250212122635668.png)

#### 5. 完成后使用 "塌陷" 保存修改

> ![image-20250212122811226](./Image/3DMaxBaseV008/image-20250212122811226.png)![image-20250212122851484](./Image/3DMaxBaseV008/image-20250212122851484.png)

------

### 模型减面

> 先选择一条边，然后使用 `石墨工具` 隔一个选一个
>
> ![image-20250212123433965](./Image/3DMaxBaseV008/image-20250212123433965.png)
>
> 点击后就会变成这样，然后选择环形，然后 "塌陷"![image-20250212123524648](./Image/3DMaxBaseV008/image-20250212123524648.png)![image-20250212123626879](./Image/3DMaxBaseV008/image-20250212123626879.png)

#### 也可以修改成隔两个选一个的

> ![image-20250212123856936](./Image/3DMaxBaseV008/image-20250212123856936.png)
>
> 这样面就会少很多了：![image-20250212123951171](./Image/3DMaxBaseV008/image-20250212123951171.png)

------

### 使用 "快速切线" 功能

> 比如制作不规则地砖
>
> ![image-20250212143626405](./Image/3DMaxBaseV008/image-20250212143626405.png)

------

### 镂空栅栏的类似做法

> 比如这个<img src="./Image/3DMaxBaseV008/Screenshot_2025-02-12-14-42-34-031_com.baidu.netdisk-edit.jpg" alt="Screenshot_2025-02-12-14-42-34-031_com.baidu.netdisk-edit" style="zoom:33%;" />
>
> 可以先切出面，然后使用桥![Screenshot_2025-02-12-12-48-00-548_com.baidu.netdisk-edit](./Image/3DMaxBaseV008/Screenshot_2025-02-12-12-48-00-548_com.baidu.netdisk-edit.jpg)

------

