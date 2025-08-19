
------

#### [返回菜单](../ALS_Menu.md)

------

# ALSv4复刻v005 创建调试Debug、输入映射、目前的摄像机系统分步骤解释

------

## 目录

- [ALSv4复刻v005 创建调试Debug、输入映射、目前的摄像机系统分步骤解释](#alsv4复刻v005-创建调试debug输入映射目前的摄像机系统分步骤解释)
  - [目录](#目录)
  - [先创建调试Debug](#先创建调试debug)
  - [接下来创建输入映射](#接下来创建输入映射)
  - [目前效果gif](#目前效果gif)
  - [接下来我将目前所做的摄像机系统分步骤解释一下](#接下来我将目前所做的摄像机系统分步骤解释一下)
    - [下面着重说一下`ALS_PlayerCameraManager::BlueprintUpdateCamera`中的数据计算顺序](#下面着重说一下als_playercameramanagerblueprintupdatecamera中的数据计算顺序)


------

<details>
<summary>视频链接</summary>

> [高级运动系统解耦和复刻第五期_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ja41197XQ?spm_id_from=333.788.videopod.episodes&vd_source=9e1e64122d802b4f7ab37bd325a89e6c&p=8)

------

</details>

------

## 先创建调试Debug

![image-20250818033211135](./Image/ALSv4Reproduce_v005/image-20250818033211135.png)![BPGraphScreenshot_2025Y-08M-18D-03h-52m-08s-547_00](./Image/ALSv4Reproduce_v005/BPGraphScreenshot_2025Y-08M-18D-03h-52m-08s-547_00.png)

------

## 接下来创建输入映射

我这里使用**增强输入**做了

插件版是有的

1. ALS_Base_CharacterBP中创建两个变量：
   - `float` 类型变量，命名为：`LookUpDownRate` = `1.25f`
   - `float` 类型变量，命名为：`LookLeftRightRate` = `1.25f`
2. 计算一下输入映射和旋转

![image-20250818033450062](./Image/ALSv4Reproduce_v005/image-20250818033450062.png)![image-20250818035331560](./Image/ALSv4Reproduce_v005/image-20250818035331560.png)![BPGraphScreenshot_2025Y-08M-18D-04h-10m-41s-184_00](./Image/ALSv4Reproduce_v005/BPGraphScreenshot_2025Y-08M-18D-04h-10m-41s-184_00.png)

------

## 目前效果gif

![2025-08-18 04-12-54](./Image/ALSv4Reproduce_v005/2025-08-18 04-12-54.gif)

------

## 接下来我将目前所做的摄像机系统分步骤解释一下

下面为分布链接跳转：

1. [新建`ALS_PlayerCameraManager`类](./ALSv4Reproduce_v002.md#三、新建CameraManager类)

2. [创建蓝图接口`ALS_Camera_BPI`，用来从角色传递参数到`CameraManager`](./ALSv4Reproduce_v002.md#创建蓝图接口ALS_Camera_BPI), [角色蓝图子类重写了接口方法](./ALSv4Reproduce_v002.md#子类重写三个接口方法)

3. 为摄像机创建动画蓝图`ALS_PlayerCameraBehavior`, 方便设置和通过ABP统一管理修改曲线
   - [为摄像机创建动画蓝图](./ALSv4Reproduce_v003.md#为摄像机创建动画蓝图ALS_PlayerCameraBehavior)
   - [在相机的骨骼网格体中添加曲线](./ALSv4Reproduce_v003.md#在相机的骨骼网格体中添加曲线)
   - [通过`ALS_PlayerCameraManager::BlueprintUpdateCamera`更新](./ALSv4Reproduce_v003.md#ALS_PlayerCameraManager中重写方法BlueprintUpdateCamera)

4. [创建方法`GetCameraBehaviorParam`，获取摄像机ABP的曲线数据](./ALSv4Reproduce_v003.md#ALS_PlayerCameraManager中创建纯函数，返回摄像机ABP的曲线参数)

### 下面着重说一下`ALS_PlayerCameraManager::BlueprintUpdateCamera`中的数据计算顺序

1. [通过接口获取玩家蓝图中配置的数据](./ALSv4Reproduce_v003.md#新建计算相机参数的函数)
2. [使用插值过渡当前角度到`ControlRotation`, 获取插值后的当前摄像机角度](./ALSv4Reproduce_v003.md#ALS_PlayerCameraManager中创建纯函数，返回摄像机ABP的曲线参数), [叠加Debug层](./ALSv4Reproduce_v004.md#)
3. [计算当前相机插值平滑后的锚点Transform](./ALSv4Reproduce_v004.md#从玩家蓝图获取摄像机锚点变换信息计算过渡信息储存在ALS_PlayerCameraManager中)
   - [这里有一个新增方法`CalculateAxisLndependentLag`不计算Roll和Pitch的过渡, 只计算Yaw的旋转，将相机位置转换为相对坐标后，插值后再加回世界坐标](./ALSv4Reproduce_v004.md#从玩家蓝图获取摄像机锚点变换信息计算过渡信息储存在ALS_PlayerCameraManager中)

4. [计算**凝视点**位置`PivotLocation`, 通过插值平滑后的锚点Transform`SmoothTargetPivot`加上下面的三条曲线的偏移量获取偏移后的**相机凝视点**`PivotLocation`](./ALSv4Reproduce_v004.md#计算凝视点位置PivotLocation)
   - **`PivotOffset_X`**
   - **`PivotOffset_Y`**
   - **`PivotOffset_Z`**

5. [相机凝视点 + 偏移量 (下面三条曲线) + 叠加Debug层 = 相机位置](./ALSv4Reproduce_v004.md#接下来在凝视点位置PivotLocation基础上加上摄像机臂的偏移，叠加Debug偏移层最终计算出摄像机位置)
   - **`CameraOffset_X`**
   - **`CameraOffset_Y`**
   - **`CameraOffset_Z`**
6. [射线检测计算当摄像机被墙阻挡后的偏移位置](./ALSv4Reproduce_v004.md#接下来要进行射线检测计算当摄像机被墙阻挡时的偏移后位置)
   - 需要注意下： **`HitResult`中`InitialOverlap`的作用?** 
7. [返回摄像机相关参数并用于`BlueprintUpdateCamera`, 一共返回了如下三个参数：](./ALSv4Reproduce_v004.md#返回摄像机相关参数并用于BlueprintUpdateCamera)
   - `FVector`类型：`Location`
   - `FRotator`类型：`Rotation`
   - `float`类型：`FOV`



------

[返回最上面](#返回菜单)

___________________________________________________________________________________________
