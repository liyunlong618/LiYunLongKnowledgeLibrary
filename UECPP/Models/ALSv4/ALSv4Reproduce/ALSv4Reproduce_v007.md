
------

#### [返回菜单](../ALS_Menu.md)

------

# ALSv4复刻v007 简述项目枚举的作用；新建接口传递玩家BP数据和状态到玩家ABP

------

## 目录

- [ALSv4复刻v007 标题](#alsv4复刻v007-标题)
  - [目录](#目录)
  - [介绍一下所有的枚举和作用](#介绍一下所有的枚举和作用)
  - [新建接口`ALS_Character_BPI`](#新建接口als_character_bpi)
  - [玩家基类`ALS_Base_CharacterBP`中继承接口`ALS_Character_BPI`重写方法](#玩家基类als_base_characterbp中继承接口als_character_bpi重写方法)
    - [玩家基类`ALS_Base_CharacterBP`中创建枚举值变量](#玩家基类als_base_characterbp中创建枚举值变量)
  - [创建玩家动画蓝图](#创建玩家动画蓝图)
  - [玩家ABP中，创建新的事件图表](#玩家abp中创建新的事件图表)
  - [通过接口`ALS_Character_BPI`的API获取玩家BP数据并缓存为变量](#通过接口als_character_bpi的api获取玩家bp数据并缓存为变量)


------

<details>
<summary>视频链接</summary>

> [高级运动系统解耦和复刻第七期_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ja41197XQ?share_source=copy_web&vd_source=ccfefcf8d65f5d070c57cddf34c94047&p=10&spm_id_from=333.788.videopod.episodes)

------

</details>

------

## 介绍一下所有的枚举和作用

```
/Data/Enums
```

```mermaid
classDiagram
direction TB
    class ALS_Gait {
        Walking /*走路中*/
        Running /*跑步*/
        Sprinting /*冲刺*/
    }

    class ALS_MovementAction {
        <<运动的动作>>
        None /*默认值*/
        LowMantle /*矮墙*/
        HighMantle /*高墙*/
        Rolling /*翻滚*/
        GettingUp /*起身*/
    }

    class ALS_MovementState {
        <<运动状态>>
        None /*默认值*/
        Grounded /*地面移动状态*/
        InAir /*空中状态*/
        Mantling /*攀爬边缘障碍物的动画过程（禁用输入/移动）*/
        Ragdoll /*在布娃娃模式*/
    }

    class ALS_OverlayState {
        <<叠加态>>
        Default /*默认状态*/
        Masculine /*用于区分角色性别对应的动画差异*/
        Feminine /*用于区分角色性别对应的动画差异 女性行走*/
        Injured /*受伤状态*/
        HandsTied /*手被绑住的状态*/
        Rifle /*持有步枪的状态*/
        Pistol 1H /*单手持有手枪的状态*/
        Pistol 2H /*双手持有手枪的状态*/
        Bow /*持有弓箭的状态*/
        Torch /*持有火把的状态*/
        Binoculars /*使用双筒望远镜的状态*/
        Box /*搬运箱子的状态*/
        Barrel /*搬运桶的状态*/
    }
```

```mermaid
classDiagram
direction TB

class ALS_RotationMode {
        <<朝哪个方向旋转>>
        VelocityDirection /*速度的方向*/
        LookingDirection /*看的方向*/
        Aiming /*动画方向*/
    }

class ALS_Stance {
        <<姿态>>
        Standing /*站立*/
        Crouching /*蹲下*/
    }
    
class ALS_ViewMode {
	<<视角模式>>
    ThirdPerson /*第三人称*/
    FirstPerson /*第一人称*/
    }

class AnimFeatureExample {
    <<动画混合相关>>
    Stride Blending /*步幅混合 解决不同速度下的步伐过渡问题*/
    Additive Leaning /*叠加倾斜 用于转弯时的上半身姿态调整*/
    Sprint Impulse /*冲刺脉冲 处理冲刺时的步态力度反馈*/
}

```



```mermaid
classDiagram
direction TB

class FootstepType {
    <<脚步类型>>
    Step /*轻微动作*/
    Walk/Run /*行走/奔跑*/
    Jump /*起跳*/
    Land /*落地*/
}

class GroundedEntryState {
    <<接地状态>>
    None /*无*/
    Roll /*翻滚*/
}

class HipsDirection {
    <<人物运动的朝向>>
    F
    B
    RF
    RB
    LF
    LB
}

class MantleType {
    <<翻墙时的墙壁类型>>
    HighMantle /*高墙*/
    LowMantle /*矮墙*/
    FallingCatch /*掉落时抓住*/
}

class MovementDirection {
    <<移动方向>>
    Forward
    Right
    Left
    Backward
}
```

------

## 新建接口`ALS_Character_BPI`

为了从`玩家BP`传递数据到`玩家ABP`

新增方法并调整分组为`CharacterInformation`：

1. `BPl_Get_CurrentState`，下面是**返回值**
   - `EMovementMode`类型变量，命名为：`PawnMovementMode`(移动模式)，移动组件中自带的
   - `ALS_MovementState`类型变量，命名为：`MovementState`
   - `ALS_MovementState`类型变量，命名为：`PrevMovementState`
   - `ALS_MovementAction`类型变量，命名为：`MovementAction`
   - `ALS_RotationMode`类型变量，命名为：`RotationMode`
   - `ALS_Gait`类型变量，命名为：`ActualGait`
   - `ALS_Stance`类型变量，命名为：`ActualStance`
   - `ALS_ViewMode`类型变量，命名为：`ViewMode`
   - `ALS_OverlayState`类型变量，命名为：`OverlayState`
2. `BPI_GetEssentialValues`
   - `FVector`类型变量，命名为：`Velocity`
   - `FVector`类型变量，命名为：`Acceleration`
   - `FVector`类型变量，命名为：`MovementInput`
   - `bool`类型变量，命名为：`IsMoving`
   - `bool`类型变量，命名为：`HasMovementInput`
   - `float`类型变量，命名为：`Speed`
   - `float`类型变量，命名为：`MovementInputAmount`
   - `FRotator`类型变量，命名为：`AimingRotation`
   - `float`类型变量，命名为：`AnimYawRate`

![image-20250819221902116](./Image/ALSv4Reproduce_v007/image-20250819221902116.png)

------

## 玩家基类`ALS_Base_CharacterBP`中继承接口`ALS_Character_BPI`重写方法

![BPGraphScreenshot_2025Y-08M-19D-22h-21m-16s-668_00](./Image/ALSv4Reproduce_v007/BPGraphScreenshot_2025Y-08M-19D-22h-21m-16s-668_00.png)

------

### 玩家基类`ALS_Base_CharacterBP`中创建枚举值变量

分组为`StateValues`

1. `ALS_MovementState`类型变量，命名为：`MovementState`
2. `ALS_MovementState`类型变量，命名为：`PrevMovementState`
3. `ALS_MovementAction`类型变量，命名为：`MovementAction`
4. `ALS_RotationMode`类型变量，命名为：`RotationMode`
5. `ALS_Gait`类型变量，命名为：`Gait`
6. `ALS_Stance`类型变量，命名为：`Stance`
7. `ALS_ViewMode`类型变量，命名为：`ViewMode`
8. `ALS_OverlayState`类型变量，命名为：`OverlayState`

![image-20250819222635507](./Image/ALSv4Reproduce_v007/image-20250819222635507.png)![BPGraphScreenshot_2025Y-08M-19D-22h-28m-58s-825_00](./Image/ALSv4Reproduce_v007/BPGraphScreenshot_2025Y-08M-19D-22h-28m-58s-825_00.png)

------

## 创建玩家动画蓝图

路径：

```
/CharacterAssets/MannequinSkeleton/
```

1. 创建动画蓝图，命名为：`ALS_AnimBP`
2. 别忘了把动画蓝图赋给`ALS_Base_CharacterBP`中的`SkeletalMeshCompoennt`

![image-20250819223503947](./Image/ALSv4Reproduce_v007/image-20250819223503947.png)

------

## 玩家ABP中，创建新的事件图表

命名为：`UpdateGraph`

1. 将`BlueprintUpdateAnimation`的参数`DeltaTimeX`存为变量
2. ABP初始化时，缓存角色变量（`Character`类型就可以）
3. 新增方法`UpdateCharacterInformation`，用来获取在玩家BP那边计算的信息

![BPGraphScreenshot_2025Y-08M-19D-22h-45m-14s-575_00](./Image/ALSv4Reproduce_v007/BPGraphScreenshot_2025Y-08M-19D-22h-45m-14s-575_00.png)![BPGraphScreenshot_2025Y-08M-19D-22h-46m-28s-909_00](./Image/ALSv4Reproduce_v007/BPGraphScreenshot_2025Y-08M-19D-22h-46m-28s-909_00.png)

------

## 通过接口`ALS_Character_BPI`的API获取玩家BP数据并缓存为变量

![BPGraphScreenshot_2025Y-08M-19D-22h-48m-31s-948_00](./Image/ALSv4Reproduce_v007/BPGraphScreenshot_2025Y-08M-19D-22h-48m-31s-948_00.png)

[返回最上面](#返回菜单)

___________________________________________________________________________________________
