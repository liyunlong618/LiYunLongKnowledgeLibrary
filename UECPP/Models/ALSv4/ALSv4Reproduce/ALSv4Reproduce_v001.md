
------

###### [返回菜单](../ALS_Menu.md)

------

# ALSv4复刻v001 删除要复刻的文件；介绍虚拟骨骼和项目Debug操作

------

## 目录

[TOC]

------

<details>
<summary>视频链接</summary>

> [高级运动系统解耦和复刻第一期_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ja41197XQ?spm_id_from=333.788.videopod.episodes&p=2)

------

</details>

------

> ## 我这里使用**UE5.5**来使用
>
> 在Github上拉取ALSv4的插件版，链接如下
>
> [DEDE-Game/ALSV4-Metahumans: UE5 - Metahuman Advanced Locomotion System](https://github.com/DEDE-Game/ALSV4-Metahumans)

------

### 3C相关UP推荐

> [五谷延年的个人空间-五谷延年个人主页-哔哩哔哩视频](https://space.bilibili.com/471422012?spm_id_from=333.337.0.0)
>
> [开发游戏的老王-CSDN博客](https://blog.csdn.net/ttm2d)
>
> [01.游戏引擎导论 | GAMES104-现代游戏引擎：从入门到实践_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1oU4y1R7Km/?spm_id_from=333.337.search-card.all.click)

------

## 介绍一下文件夹结构

> ```
> AdvanceLocomotionSystemV4/
> ├─ Audio/
> │  ├─ Background/    # BGM
> │  ├─ Footsteps/     # 脚步声
> │  └─ UI/            # 按键声
> ├─ Blueprints/
> │  ├─ AnimModifiers/    # 动画修改器（多用于转向动画）
> │  ├─ AnimNotifys/      # 行走时脚步声触发
> │  ├─ CameraSystem/     # 曲线混合摄像机位置 + SK 模型
> │  ├─ CharacterLogic/   # 玩家 & AI 逻辑
> │  ├─ Components/		# 这个是和蓝图版的区别 蓝图版没有
> │  │  ├─ DebugComponent   # 调试组件
> │  │  └─ MantleComponent  # 检测地形攀爬
> │  ├─ GameModes/          # 游戏模式
> │  ├─ Input/              # 增强输入
> │  ├─ Interfaces/         # 四个接口: 连接了 玩家/控制器/摄像机/人物蓝图
> │  ├─ Libraries/          # 工具函数库
> │  ├─ Misc/				  # 杂项 Miscellaneous的缩写
> │  │  └─ Sprint_CameraShake  # 冲刺时的摄像机抖动
> │  └─ UI/                 # 界面UI
> ├─ CharacterAssets/
> │  └─ MannequinSkeleton/
> │     ├─ AnimationExamples/
> │     │  ├─ Actions/      # 过渡动画资产（含蒙太奇）
> │     │  └─ AimOffsets/   # 瞄准偏移资源
> │     ├─ Base/			  # 序列动画
> │     │  ├─ BasePoses/    
> │     │  ├─ InAir/        
> │     │  ├─ Locomotion/   # 基础运动
> │     │  │	└─ # 有六个混合动画:B/BLBR/F/FL/FR	对应六个方向 没有正左和正右
> │     │  ├─ Transitions/  
> │     │  └─ TurnInPlace/  
> │     ├─ Overlay/         
> │     ├─ ALS_AnimBP       # 动画蓝图
> │     └─ ALS_Mannequin_Skeleton  # 人物骨骼资源
> ├─ Data/                  # 数据表
> │  ├─ Curves/
> │  ├─ DataTables/
> │  ├─ Enums/
> │  └─ Structs/
> ├─ Environment/           # 感觉是交互的道具
> ├─ Levels/                # 关卡地图
> └─ Props/                 # 场景道具与材质
>    ├─ Materials/
>    └─ Meshes/
> ```
>

------

## 下面开始删除要复刻的文件

> ```
> AdvanceLocomotionSystemV4/
> ├─ Audio/
> │  ├─ Background/
> │  ├─ Footsteps/
> │  └─ UI/    
> ├─ Blueprints/
> │  ├─ AnimModifiers/	# 删除AnimModifiers下的所有动画修改器
> │  ├─ AnimNotifys/ 		# 删除AnimNotifys下的所有动画修改器
> │  ├─ CameraSystem/		# 删除CameraSystem下的`动画蓝图`和`摄像机曲线`
> │  ├─ CharacterLogic/	# 删除CharacterLogic下的所有蓝图和AI文件夹
> │  ├─ Components/
> │  │  ├─ DebugComponent
> │  │  └─ MantleComponent
> │  ├─ GameModes/		# 删除GameModes下的GM
> │  ├─ Input/
> │  ├─ Interfaces/  		# 删除Interfaces下的四个接口
> │  ├─ Libraries/		# 删除Libraries下的蓝图函数库
> │  ├─ Misc/				# 删除Misc下的摄相机抖动文件
> │  │  └─ Sprint_CameraShake # 删除这个 
> │  └─ UI/                 
> ├─ CharacterAssets/
> │  └─ MannequinSkeleton/
> │     ├─ AnimationExamples/
> │     │  ├─ Actions/    # 删除Actions下的蒙太奇文件
> │     │  └─ AimOffsets/ # 删除AimOffsets下的瞄准偏移
> │     ├─ Base/			  
> │     │  ├─ BasePoses/    
> │     │  ├─ InAir/      # 删除InAir的Detail下的混合空间 
> │     │  ├─ Locomotion/ # 删除Locomotion和Detail下的混合空间
> │     │  ├─ Transitions/  
> │     │  └─ TurnInPlace/  
> │     ├─ Overlay/         
> │     ├─ ALS_AnimBP		# 删除MannequinSkeleton下的ALS_AnimBP
> │     └─ ALS_Mannequin_Skeleton  # 删除`ALS_Mannequin_Skeleton`人物骨骼中的曲线
> ├─ Data/                  
> │  ├─ Curves/
> │  ├─ DataTables/
> │  ├─ Enums/
> │  └─ Structs/
> ├─ Environment/      
> ├─ Levels/
> └─ Props/
>    ├─ Materials/
>    └─ Meshes/
> ```

------

### 删除AnimModifiers下的所有动画修改器

大部分用于转向动画

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/Blueprints/AnimModifiers
```

![image-20250804224017041](./Image/ALSv4Reproduce_v001/image-20250804224017041.png)

------

### 删除AnimNotifys下的所有动画修改器

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/Blueprints/AnimNotifys
```

![image-20250804224132168](./Image/ALSv4Reproduce_v001/image-20250804224132168.png)

------

### 删除CameraSystem下的`动画蓝图`和`摄像机曲线`

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/Blueprints/CameraSystem
```

![image-20250804224356405](./Image/ALSv4Reproduce_v001/image-20250804224356405.png)

### 删除摄像机曲线

![image-20250804224710956](./Image/ALSv4Reproduce_v001/image-20250804224710956.png)![image-20250804224604928](./Image/ALSv4Reproduce_v001/image-20250804224604928.png)

------

### 删除CharacterLogic下的所有蓝图和AI文件夹

**AI暂时不涉及，以后有机会再深入学习**

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/Blueprints/CharacterLogic
```

![image-20250804224942402](./Image/ALSv4Reproduce_v001/image-20250804224942402.png)

------

### 删除GameModes下的GM

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/Blueprints/GameModes
```

![image-20250804225039672](./Image/ALSv4Reproduce_v001/image-20250804225039672.png)

------

### 删除Interfaces下的四个接口

连接了 玩家/控制器/摄像机/人物蓝图

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/Blueprints/Interfaces
```

![image-20250804225216184](./Image/ALSv4Reproduce_v001/image-20250804225216184.png)

------

### 删除Libraries下的蓝图函数库

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/Blueprints/Libraries
```

![image-20250804225310308](./Image/ALSv4Reproduce_v001/image-20250804225310308.png)

------

### 删除Misc下的摄相机抖动文件

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/Blueprints/Misc
```

![image-20250804225402377](./Image/ALSv4Reproduce_v001/image-20250804225402377.png)

------

### 删除MannequinSkeleton下的ALS_AnimBP

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/CharacterAssets/MannequinSkeleton
```

![image-20250804225523009](./Image/ALSv4Reproduce_v001/image-20250804225523009.png)

------

### 删除Actions下的蒙太奇文件

**注意不要错删动画文件！**

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/CharacterAssets/MannequinSkeleton/AnimationExamples/Actions
```

![image-20250804225657569](./Image/ALSv4Reproduce_v001/image-20250804225657569.png)

------

### 删除AimOffsets下的瞄准偏移 

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/CharacterAssets/MannequinSkeleton/AnimationExamples/AimOffsets
```

![image-20250804225819513](./Image/ALSv4Reproduce_v001/image-20250804225819513.png)

------

### 删除InAir的Detail下的混合空间

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/CharacterAssets/MannequinSkeleton/AnimationExamples/Base/InAir/Detail
```

![image-20250804225917743](./Image/ALSv4Reproduce_v001/image-20250804225917743.png)

------

### 删除Locomotion和Detail下的混合空间

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/CharacterAssets/MannequinSkeleton/AnimationExamples/Base/Locomotion
```

![image-20250804230039216](./Image/ALSv4Reproduce_v001/image-20250804230039216.png)![image-20250804230106502](./Image/ALSv4Reproduce_v001/image-20250804230106502.png)

------

### 删除`ALS_Mannequin_Skeleton`人物骨骼中的曲线

```
/All/Plugins/ALSV4_CPP/AdvancedLocomotionV4/CharacterAssets/MannequinSkeleton
```

![image-20250804230255672](./Image/ALSv4Reproduce_v001/image-20250804230255672.png)![image-20250804230327089](./Image/ALSv4Reproduce_v001/image-20250804230327089.png)

------

## 删除完毕

------

## 介绍一下虚拟骨骼

![image-20250804230524688](./Image/ALSv4Reproduce_v001/image-20250804230524688.png)

虚拟骨骼可以模仿IK骨骼

### 创建虚拟骨骼

![image-20250804230751693](./Image/ALSv4Reproduce_v001/image-20250804230751693.png)![image-20250804230850807](./Image/ALSv4Reproduce_v001/image-20250804230850807.png)

------

## 还有一些没删除的东西，比如：

- 动画通知
- 动画中的配置
  - 比如启用根运动
  - 强制根锁定

伴随着用的时候介绍

------



------

## 简单介绍一下ALSv4的相关操作

|      | 按键 | 作用                                                         |
| ---- | ---- | ------------------------------------------------------------ |
|      | Z    |                                                              |
|      | V    |                                                              |
|      | T    | 检测墙体是否可以攀爬，检测落地；胶囊体为检测摄像机和玩家之间是否有障碍，修正摄像机位置 |
|      | Y    | 可视化调试                                                   |
|      | U    | 混合系统查看                                                 |
|      | I    | 查看各项参数                                                 |

其他是一些操作按键

![image-20250804233313264](./Image/ALSv4Reproduce_v001/image-20250804233313264.png)

### Y可视化调试介绍

#### 蓝色箭头为当前玩家Mesh朝向![image-20250804232133161](./Image/ALSv4Reproduce_v001/image-20250804232133161.png)

#### 橙色箭头为按键映射输入方向

开启Slomo后观察更明显

![image-20250804232248446](./Image/ALSv4Reproduce_v001/image-20250804232248446.png)

#### 紫色箭头为当前移动的加速度

开启Slomo后观察更明显

会缓慢追上橙色箭头

![image-20250804232356130](./Image/ALSv4Reproduce_v001/image-20250804232356130.png)

### U混合系统查看`观察到混合过程`

**按U开启 -> 按下Q切换到望远镜 -> 按下右键可以观察到混合过程**

![image-20250804232829418](./Image/ALSv4Reproduce_v001/image-20250804232829418.png)![image-20250804232841153](./Image/ALSv4Reproduce_v001/image-20250804232841153.png)

------

[返回最上面](#返回菜单)

___________________________________________________________________________________________
