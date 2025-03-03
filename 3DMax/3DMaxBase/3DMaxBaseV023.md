
___________________________________________________________________________________________
###### [GoMenu](../3DMaxBasicsMenu.md)
___________________________________________________________________________________________
# 023_材质分层介绍、使用SubStance上材质、锈迹、贴纸、喷绘字体、玻璃材质、渲染图片、导出贴图纹理


___________________________________________________________________________________________


## 目录

[TOC]


------

## 材质分层

> 金属材质分层：
>
> 1. 基础颜色（金属质感）
> 2. 掉漆
> 3. 脏旧
> 4. 锈迹
>
> ![fd57ee2366621d4c11b0904a3736fbd6_origin(1)](./Image/3DMaxBaseV023/fd57ee2366621d4c11b0904a3736fbd6_origin(1).jpg)![Screenshot_2025-03-03-20-33-37-238_com.baidu.netdisk-edit](./Image/3DMaxBaseV023/Screenshot_2025-03-03-20-33-37-238_com.baidu.netdisk-edit.jpg)

------

## 使用SubStance上材质

### 导入流程

> ![image-20250303201836191](./Image/3DMaxBaseV023/image-20250303201836191.png)![image-20250303202144340](./Image/3DMaxBaseV023/image-20250303202144340.png)

### 烘焙其他辅助贴图

> ![image-20250303202335950](./Image/3DMaxBaseV023/image-20250303202335950.png)![image-20250303202548544](./Image/3DMaxBaseV023/image-20250303202548544.png)

------

### 上基础材质

> 1. 新建组
> 2. 新建填充层->填充红色
> 3. 新建黑色遮罩
> 4. 选择几何体填充
>
> ![image-20250303203508868](./Image/3DMaxBaseV023/image-20250303203508868.png)![image-20250303203550339](./Image/3DMaxBaseV023/image-20250303203550339.png)![image-20250303203707411](./Image/3DMaxBaseV023/image-20250303203707411.png)![image-20250303203805062](./Image/3DMaxBaseV023/image-20250303203805062.png)![image-20250303203929771](./Image/3DMaxBaseV023/image-20250303203929771.png)![image-20250303204112645](./Image/3DMaxBaseV023/image-20250303204112645.png)![image-20250303204513178](./Image/3DMaxBaseV023/image-20250303204513178.png)

### 使用基础材质

使用这个材质的好处是自带划痕和金属磨损

> ![image-20250304002714254](./Image/3DMaxBaseV023/image-20250304002714254.png)![image-20250304002946303](./Image/3DMaxBaseV023/image-20250304002946303.png)

#### 可以使用Height制作凸起和凹槽

> ![image-20250304003328097](./Image/3DMaxBaseV023/image-20250304003328097.png)![image-20250304004024112](./Image/3DMaxBaseV023/image-20250304004024112.png)

#### 界面其他属性

> ![image-20250304003454730](./Image/3DMaxBaseV023/image-20250304003454730.png)![image-20250304003704839](./Image/3DMaxBaseV023/image-20250304003704839.png)

#### 画笔模式`绘制直线`,按住Shift

> ![image-20250304003850527](./Image/3DMaxBaseV023/image-20250304003850527.png)

#### 画笔调整旋转方向按住`Ctrl+左键`

#### 旋转HDR：`Shift+右键`

------

#### 可以单独制作突起和凹槽图案

> ![image-20250304005345059](./Image/3DMaxBaseV023/image-20250304005345059.png)![image-20250304005425010](./Image/3DMaxBaseV023/image-20250304005425010.png)

------

### 根据原画调节粗糙度和高光

> ![image-20250304005817166](./Image/3DMaxBaseV023/image-20250304005817166.png)

### 制作边缘磨损材质

> 1. 先来个磨损材质（倒数第八个）
> 2. 使用智能遮罩（拖拽到磨损图层上）
>    - 调整智能遮罩参数
> 3. 手绘调整智能遮罩
>    - 使用透贴绘制模拟剐蹭的效果
>    - 可以擦去一些剐蹭，让整体更自然
> 4. 常用的关节处，磨损会稍微严重些，可以画一画
>
> 
>
> ![image-20250304011415149](./Image/3DMaxBaseV023/image-20250304011415149.png)![image-20250304011142413](./Image/3DMaxBaseV023/image-20250304011142413.png)![image-20250304011606714](./Image/3DMaxBaseV023/image-20250304011606714.png)![image-20250304011811867](./Image/3DMaxBaseV023/image-20250304011811867.png)![image-20250304011924102](./Image/3DMaxBaseV023/image-20250304011924102.png)![image-20250304012036173](./Image/3DMaxBaseV023/image-20250304012036173.png)![image-20250304012249787](./Image/3DMaxBaseV023/image-20250304012249787.png)![image-20250304012353110](./Image/3DMaxBaseV023/image-20250304012353110.png)

#### 为磨损材质添加一些厚度

> ![image-20250304012723226](./Image/3DMaxBaseV023/image-20250304012723226.png)![image-20250304013014140](./Image/3DMaxBaseV023/image-20250304013014140.png)

------

### 制作物体关系（缝隙中的脏迹）

> ![image-20250304013721862](./Image/3DMaxBaseV023/image-20250304013721862.png)![image-20250304013952313](./Image/3DMaxBaseV023/image-20250304013952313.png)![image-20250304014112087](./Image/3DMaxBaseV023/image-20250304014112087.png)

### 制作漏油的物体关系（使用粒子笔刷）

> 可以复制物体关系这层，颜色在深一些，使用粒子笔刷
>
> ![image-20250304014636574](./Image/3DMaxBaseV023/image-20250304014636574.png)

### 手绘部分材质

> ![image-20250304015447257](./Image/3DMaxBaseV023/image-20250304015447257.png)![image-20250304015523569](./Image/3DMaxBaseV023/image-20250304015523569.png)

### 制作锈迹

> **一般出现在关节衔接处**
>
> 1. 找一个锈迹的材质
> 2. 使用智能遮罩
> 3. 添加智能滤镜
> 4. 调整一下智能滤镜参数
>
> ![image-20250304020655818](./Image/3DMaxBaseV023/image-20250304020655818.png)![image-20250304020822652](./Image/3DMaxBaseV023/image-20250304020822652.png)![image-20250304021657727](./Image/3DMaxBaseV023/image-20250304021657727.png)![image-20250304021737373](./Image/3DMaxBaseV023/image-20250304021737373.png)![image-20250304021845864](./Image/3DMaxBaseV023/image-20250304021845864.png)

### 制作贴纸

> 1. PS中制作，对好位置
> 2. 导入SubStance
> 3. 但是填充层会挡住别的层的效果所以需要调节质感
> 4. 然后再给贴纸的填充层添加黑色遮罩使用笔刷，将要的贴纸区域绘制蒙版
>
> ![image-20250304021137032](./Image/3DMaxBaseV023/image-20250304021137032.png)![image-20250304021239379](./Image/3DMaxBaseV023/image-20250304021239379.png)![image-20250304021351349](./Image/3DMaxBaseV023/image-20250304021351349.png)![image-20250304021522727](./Image/3DMaxBaseV023/image-20250304021522727.png)

------

### 喷绘字体

> 使用默认笔刷
>
> 透贴选择指定的这几个字体之一（名中有font的）
>
> ![image-20250304020351951](./Image/3DMaxBaseV023/image-20250304020351951.png)

------

### 玻璃材质

> 1. 还是使用倒数第七个材质
> 2. 关闭金属度
> 3. 颜色为灰色偏绿
> 4. 金属粗糙度（应该不粗糙）
>
> ![image-20250304022540718](./Image/3DMaxBaseV023/image-20250304022540718.png)![image-20250304022606910](./Image/3DMaxBaseV023/image-20250304022606910.png)![image-20250304022635936](./Image/3DMaxBaseV023/image-20250304022635936.png)![image-20250304022711525](./Image/3DMaxBaseV023/image-20250304022711525.png)![image-20250304022752103](./Image/3DMaxBaseV023/image-20250304022752103.png)![image-20250304022823985](./Image/3DMaxBaseV023/image-20250304022823985.png)

#### 添加玻璃划痕

> 1. 只保留粗糙度
> 2. 选择一张划痕的黑白图
> 3. 缩小UV比例
>
> ![image-20250304022940340](./Image/3DMaxBaseV023/image-20250304022940340.png)![image-20250304023031445](./Image/3DMaxBaseV023/image-20250304023031445.png)![image-20250304023112141](./Image/3DMaxBaseV023/image-20250304023112141.png)

#### 添加玻璃灰尘

> 1. 选一个土的材质
> 2. 不要高度
> 3. 比例缩小
> 4. 点状强度小一些
> 5. 颜色暗一些
> 6. 破璃的灰尘一般出现在边缘:
>    - 加一个边缘的智能遮罩
>    - 调整强度、纹理和不透明度
> 7. 使用点状笔刷，点一些玻璃上的脏点
> 8. 与别的结构衔接处可以手动，画一些灰尘
>
> ![image-20250304023227062](./Image/3DMaxBaseV023/image-20250304023227062.png)![image-20250304023326038](./Image/3DMaxBaseV023/image-20250304023326038.png)![image-20250304023421605](./Image/3DMaxBaseV023/image-20250304023421605.png)![image-20250304023505271](./Image/3DMaxBaseV023/image-20250304023505271.png)![image-20250304023538506](./Image/3DMaxBaseV023/image-20250304023538506.png)![image-20250304023803601](./Image/3DMaxBaseV023/image-20250304023803601.png)![image-20250304023951003](./Image/3DMaxBaseV023/image-20250304023951003.png)![image-20250304024137614](./Image/3DMaxBaseV023/image-20250304024137614.png)

------

## SubStance渲染图片

> ![image-20250304024639122](./Image/3DMaxBaseV023/image-20250304024639122.png)![image-20250304025341583](./Image/3DMaxBaseV023/image-20250304025341583.png)![image-20250304025509059](./Image/3DMaxBaseV023/image-20250304025509059.png)![image-20250304025856403](./Image/3DMaxBaseV023/image-20250304025856403.png)

------

## 导出贴图纹理

> 检查一下大小
>
> ![image-20250304030931254](./Image/3DMaxBaseV023/image-20250304030931254.png)![image-20250304031201077](./Image/3DMaxBaseV023/image-20250304031201077.png)![image-20250304031229889](./Image/3DMaxBaseV023/image-20250304031229889.png)![image-20250304031247358](./Image/3DMaxBaseV023/image-20250304031247358.png)![image-20250304030956279](./Image/3DMaxBaseV023/image-20250304030956279.png)![image-20250304031352954](./Image/3DMaxBaseV023/image-20250304031352954.png)![image-20250304031454114](./Image/3DMaxBaseV023/image-20250304031454114.png)

------