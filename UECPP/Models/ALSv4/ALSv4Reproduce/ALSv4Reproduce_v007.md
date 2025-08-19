
------

#### [返回菜单](../ALS_Menu.md)

------

# ALSv4复刻v007 标题

------

## 目录

[TOC]

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

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

XXXXXXXXXXXXX
------

[返回最上面](#返回菜单)

___________________________________________________________________________________________
