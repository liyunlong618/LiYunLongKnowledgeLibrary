[【返回菜单】](../ALS_Menu.md)

------

# ALSv001 项目设置

------

## 目录

[TOC]

------

- 链接：



------

> ### 使用的版本：
> 我这里使用 **UE4.26** 版本
>
> 先不考虑摄像机相关的功能，先学习动画

------

> ### 在 **第三人称模板** 的基础上做如下修改

------

### 一、新建工程

> ![image-20250102143448880](./Image/ALSv001/image-20250102143448880.png)

------

### 二、迁移资产

> 将 `Content\AdvancedLocomotionV4\CharacterAssets\MannequinSkeleton\AnimationExamples` 文件夹
>
> 迁移到自建的`ALSV4`项目中
>
> ![image-20250102144830362](./Image/ALSv001/image-20250102144830362.png)
>
> ![image-20250102145029380](./Image/ALSv001/image-20250102145029380.png)
>
> ![image-20250102145112771](./Image/ALSv001/image-20250102145112771.png)

### 三、迁移Config目录下的输入映射

> ![image-20250102145421359](./Image/ALSv001/image-20250102145421359.png)

------

> ### 完成后需要重新打开项目，Config才会生效
>
> 重新打开后，打开 **项目设置->输入** (可以看到已完成输入映射迁移)![image-20250102145727143](./Image/ALSv001/image-20250102145727143.png)

------

### 四、按照原有的文件结构，新建文件夹并配置部分关键资产

> 在 `Content\AdvancedLocomotionV4\Blueprints` 文件夹下创建 文件夹
>
> - `CharacterLogic`(存放玩家控制器) 
> - `GameModes` 
>
> ------

#### 1.创建 `PlayerController`

> `CharacterLogic`文件夹下创建 `PlayerController` (玩家控制器，继承自 `PlayerController`)
>
> - 命名为 `ALS_Player_Controller`
>
>   ![image-20250102150516131](./Image/ALSv001/image-20250102150516131.png)

------

#### 2.创建 `Character`

> `CharacterLogic`文件夹下创建 `Character` (玩家，继承自 `Character`)
>
> - 命名为 `ALS_Base_CharacterBP`
>
>   ![image-20250102152659505](./Image/ALSv001/image-20250102152659505.png)
>
> ------
>
> 创建 `Character` (玩家，继承自 `ALS_Base_CharacterBP`)
>
> - 命名为 `ALS_AnimMan_CharacterBP`
>
>   ![image-20250102152905868](./Image/ALSv001/image-20250102152905868.png)

------

#### 3.创建并配置 `GameMode`

> `GameModes`[^1] 文件夹下创建 `GameMode` (继承自 `GameMode`)
>
> - 命名为 `ALS_GameMode`
>
>   ![image-20250102154435881](./Image/ALSv001/image-20250102154435881.png)
>
> 配置 `ALS_GameMode`
>
> - ![image-20250102154656275](./Image/ALSv001/image-20250102154656275.png)![image-20250102154746364](./Image/ALSv001/image-20250102154746364.png)

------
### 五、配置角色基类 `ALS_Base_CharacterBP` 的 `SkeletalMesh` `相机` `弹簧臂`

> - 为角色基类 `ALS_Base_CharacterBP` 设置 `SkeletalMesh`![image-20250102155724015](./Image/ALSv001/image-20250102155724015.png)
>
> - 添加弹簧臂和相机组件，调整位置![image-20250102160215818](./Image/ALSv001/image-20250102160215818.png)

------

### 六、删除多余文件

> 这里只保留Maps
>
> ![image-20250102160717095](./Image/ALSv001/image-20250102160717095.png)
>
> 删除场景中的角色，并删除掉角色所在的文件夹 `Mannequin`
>
> ![image-20250102155331248](./Image/ALSv001/image-20250102155331248.png)

#### 删完以后剩这些：

![image-20250102161308970](./Image/ALSv001/image-20250102161308970.png)

------

> ### 准备工作完成

------

[^1]: `Content\AdvancedLocomotionV4\Blueprints\GameModes`