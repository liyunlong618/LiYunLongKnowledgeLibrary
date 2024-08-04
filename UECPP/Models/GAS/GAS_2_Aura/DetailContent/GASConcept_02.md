___________________________________________________________________________________________
###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________

# 概念和联网 GA(GameplayAbilities)


___________________________________________________________________________________________

# 目录


- [概念和联网 GA(GameplayAbilities)](#概念和联网-gagameplayabilities)
- [目录](#目录)
	- [GameplayAbilities](#gameplayabilities)
	- [AbilityTask](#abilitytask)
	- [联网！](#联网)
	- [整个激活技能的流程](#整个激活技能的流程)
		- [完整流程总结](#完整流程总结)
			- [详细解释](#详细解释)


___________________________________________________________________________________________

## 什么是GameplayTags

>  - 游戏标签具有层次结构。它们采用父子、孙子的形式，层次结构的个级别之间用点号分割
  - 那么为什么游戏标签如此重要呢?我们不能只使用F-string或F-name,或者也许在某些情况下只使用枚举或布尔值吗?
  - 深入了解一下 GameplayTags 的底层原理。
    - 在虚幻引擎中，GameplayTags 是通过 FGameplayTag 结构体和 FGameplayTagContainer 类来实现的。FGameplayTag 结构体表示单个标记，而 FGameplayTagContainer 则是标记的容器，可以存储多个标记。
    - 每个 GameplayTag 都由一个或多个名称组成，这些名称构成了一个层次结构，类似于文件系统中的文件路径。例如，"Character.Player.Hero" 可以表示一个角色的玩家英雄标记，其中 "Character" 是顶层标记，"Player" 是其子标记，"Hero" 是 "Player" 的子标记。
  - GameplayTags 的主要功能可以分为两个方面：标记管理和标记操作。
    - 标记管理：
      - 注册和创建： 游戏开发者可以在游戏启动时注册和创建需要的标记。通过 FGameplayTag::RequestGameplayTag() 函数可以创建一个 GameplayTag。
      - 层次结构： 标记之间可以建立层次关系，形成树状结构，方便对标记进行组织和管理。
      - 元数据： 每个标记可以关联一些元数据，比如描述信息、父标记等。
    - 标记操作：
      - 查询和比较： 可以通过 FGameplayTagContainer 类提供的函数来查询标记是否存在于容器中，或者进行标记之间的比较操作。
      - 标记集合操作： 可以对多个标记进行集合操作，包括并集、交集、差集等，以便于进行标记的组合和过滤。
      - 标记解析： 可以将字符串形式的标记路径解析成 GameplayTag，或者将 GameplayTag 转换成字符串形式的路径。
  - 两个标签可以进行精确比较，甚至部分比较。也许它们只共享相同的根标签名称，这在代码中可能很重要。

    - ![img](https://api2.mubu.com/v3/document_image/25165450_8b078506-3cdb-4cb2-e682-b4d11e1a6fbf.png)
    
    - ![img](https://api2.mubu.com/v3/document_image/25165450_93b4c600-604e-46a2-d52f-12772b5845b9.png)
    
    - ![img](https://api2.mubu.com/v3/document_image/25165450_eff31cdd-db9a-497a-cbdd-669828bb2e36.png)

___________________________________________________________________________________________

## 创建GameplayTags

有几种方法

1. 第一种 在编辑器的项目设置中，添加GamplayTag标签

- 在编辑器的项目设置中，添加GamplayTag标签

![img](https://api2.mubu.com/v3/document_image/25165450_c667e7b8-9417-4056-a549-1978c141e50e.png)

![img](https://api2.mubu.com/v3/document_image/25165450_37252b78-514d-4880-aedc-58b6ce7e0fd3.png)

- 添加后
![img](https://api2.mubu.com/v3/document_image/25165450_f5d8fd48-f568-4abd-dc58-aef72c65a36f.png)

![img](https://api2.mubu.com/v3/document_image/25165450_6822dc0c-bc6c-4231-b9b5-0f53bb6c07e8.png)

![img](https://api2.mubu.com/v3/document_image/25165450_39fa1d73-74ec-442a-aa5a-c3ad0e32467c.png)

![img](https://api2.mubu.com/v3/document_image/25165450_4f476e04-2fb8-41db-aa6f-f145449653dd.png)

2. 第二种 使用表格
    
- BP下创建AbilitySystem文件夹
![img](https://api2.mubu.com/v3/document_image/25165450_9924a7b7-e20c-4696-cbaf-9b4736d457b3.png)

- AbilitySystem文件夹下创建GameplayTags文件夹
![img](https://api2.mubu.com/v3/document_image/25165450_48d01a39-02b7-4619-fc6d-de99b48b2a1f.png)

- GameplayTags文件夹中，添加数据表格

![img](https://api2.mubu.com/v3/document_image/25165450_6506cc89-7224-46aa-d1ff-eb97e88f84e1.png)

![img](https://api2.mubu.com/v3/document_image/25165450_117e8454-de1c-41d2-dda2-5b008a0159f2.png)

![img](https://api2.mubu.com/v3/document_image/25165450_ffaac2af-2843-4c25-e9d0-70b24f25189c.png)

![img](https://api2.mubu.com/v3/document_image/25165450_8f38b3c7-6851-4f2c-c409-7c4a0aacee11.png)

![img](https://api2.mubu.com/v3/document_image/25165450_5d21313e-37d6-4425-c8d7-559691ca81b2.png)

![img](https://api2.mubu.com/v3/document_image/25165450_23570be1-ba67-47e3-cda6-4407a2f66755.png)

- 项目设置中使用自建的GamplayTags表格

![img](https://api2.mubu.com/v3/document_image/25165450_5708f3b1-4414-4dfc-cf88-183c7a7052f4.png)

![img](https://api2.mubu.com/v3/document_image/25165450_9b5ed124-7e97-4596-924e-84f06a5134ba.png)

![img](https://api2.mubu.com/v3/document_image/25165450_90afe552-b4e0-4a54-e6a6-706cb7a015af.png)

- 在项目中打开配置文件
- ![img](https://api2.mubu.com/v3/document_image/25165450_7419c3ad-fe2e-4446-8788-598f6cc4b20b.png)

- ![img](https://api2.mubu.com/v3/document_image/25165450_d65c85e8-f33f-4da4-b2d0-a4c262913f8a.png)

### 给物体添加标签，理解用的测试(如果操作，记得撤销操作)

- 理解用的测试(如果操作，记得撤销操作)

    - 给物体添加标签

      - 比如，在加血的水晶上加一个标签
		![img](https://api2.mubu.com/v3/document_image/25165450_d67b3347-4bcf-4a3a-888f-fcf4ad3c75bd.png)

      - 拾取水晶

        - 未拾取时，身上没有Tag标签![img](https://api2.mubu.com/v3/document_image/25165450_88d46ec9-d45e-475d-a153-32b2017b9677.png)

        - 拾取后，水晶持续时间内身上会持有这个刚设置的标签，持续时间结束后，该标签会被移除![img](https://api2.mubu.com/v3/document_image/25165450_09995ce0-a820-494d-e2e2-c26d105209a5.png)

#### 帮助理解：修改堆叠测试

- 修改堆叠计数为3，一次吃三个水晶，身上也只有一个Tag
![img](https://api2.mubu.com/v3/document_image/25165450_78461f5f-340a-408d-c414-4670f6c6ace4.png)

- 如果取消了堆叠，一次吃三个水晶，身上有3个Tag

![img](https://api2.mubu.com/v3/document_image/25165450_8d91d367-694b-42e6-b18b-631c7a34a6d3.png)

- 拾取前
- ![img](https://api2.mubu.com/v3/document_image/25165450_66872276-2d63-4097-82be-a76c528663d3.png)
      
- 拾取后
- ![img](https://api2.mubu.com/v3/document_image/25165450_604b5b4b-51ef-4290-910e-db7ee5d5e36f.png)

- 只有有持续时间的，添加GE下的Component下的Target Tags Gameplay Effect Component 下的Tag标签才有意义
- ![img](https://api2.mubu.com/v3/document_image/25165450_17e2cd2e-1336-444e-b255-68853faab09b.png)

- 如果是瞬时生效的需要Tag，需要加资产标签AssetTag，先了解

- RPC参考这张图
![img](https://api2.mubu.com/v3/document_image/25165450_9b79b3be-7a2f-42c4-83ce-e00e488487c8.png)

___________________________________________________________________________________________

[返回最上面](#Go主菜单)

___________________________________________________________________________________________