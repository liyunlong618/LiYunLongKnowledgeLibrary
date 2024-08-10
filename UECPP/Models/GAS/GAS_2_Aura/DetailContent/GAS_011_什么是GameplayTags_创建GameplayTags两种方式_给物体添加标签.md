___________________________________________________________________________________________

###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________

# GAS_011_什么是GameplayTags_创建GameplayTags两种方式_给物体添加标签

___________________________________________________________________________________________

# 目录
- [GAS 011 什么是GameplayTags？:创建GameplayTags两种方式:给物体添加标签](#gas-011-什么是gameplaytags创建gameplaytags两种方式给物体添加标签)
- [目录](#目录)
    - [什么是GameplayTags](#什么是gameplaytags)
      - [游戏标签具有层次结构。它们采用父子、孙子的形式,层次结构的个级别之间用 点号 分割](#游戏标签具有层次结构它们采用父子孙子的形式层次结构的个级别之间用-点号-分割)
      - [深入了解一下 GameplayTags 的底层原理。](#深入了解一下-gameplaytags-的底层原理)
      - [GameplayTags 的主要功能可以分为两个方面:标记管理和标记操作。](#gameplaytags-的主要功能可以分为两个方面标记管理和标记操作)
    - [创建GameplayTags几种方法](#创建gameplaytags几种方法)
      - [第一种 在编辑器的 项目设置 中, 添加GamplayTag标签](#第一种-在编辑器的-项目设置-中-添加gamplaytag标签)
          - [在编辑器的 项目设置 中, 添加GamplayTag标签](#在编辑器的-项目设置-中-添加gamplaytag标签)
      - [第二种 使用 表格](#第二种-使用-表格)
          - [BP 下创建 AbilitySystem 文件夹](#bp-下创建-abilitysystem-文件夹)
          - [AbilitySystem 文件夹下创建 GameplayTags 文件夹](#abilitysystem-文件夹下创建-gameplaytags-文件夹)
          - [GameplayTags 文件夹中,添加数据表格](#gameplaytags-文件夹中添加数据表格)
          - [项目设置中使用自建的GamplayTags表格](#项目设置中使用自建的gamplaytags表格)
      - [在项目中打开配置文件](#在项目中打开配置文件)
    - [给物体添加标签, 理解用的测试 (如果操作,记得撤销操作)](#给物体添加标签-理解用的测试-如果操作记得撤销操作)
      - [理解用的测试 (如果操作,记得撤销操作)](#理解用的测试-如果操作记得撤销操作)
        - [给物体添加标签](#给物体添加标签)
          - [比如,在加血的水晶上加一个标签](#比如在加血的水晶上加一个标签)
          - [拾取水晶](#拾取水晶)
          - [帮助理解: 修改堆叠测试](#帮助理解-修改堆叠测试)
        - [只有有持续时间的,添加 GE下的Component下的Target Tags Gameplay Effect Component 下的Tag标签 才有意义](#只有有持续时间的添加-ge下的component下的target-tags-gameplay-effect-component-下的tag标签-才有意义)
        - [如果是瞬时生效的需要Tag,需要加资产标签AssetTag,先了解](#如果是瞬时生效的需要tag需要加资产标签assettag先了解)
      - [RPC参考这张图](#rpc参考这张图)


___________________________________________________________________________________________


### 什么是GameplayTags 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/977836_567347.png?raw=true)
___________________________________________________________________________________________


#### 游戏标签具有层次结构。它们采用父子、孙子的形式,层次结构的个级别之间用 点号 分割
___________________________________________________________________________________________


#### 深入了解一下 GameplayTags 的底层原理。

>在虚幻引擎中,GameplayTags 是通过 FGameplayTag 结构体和 FGameplayTagContainer 类来实现的。FGameplayTag 结构体表示单个标记,而 FGameplayTagContainer 则是标记的容器,可以存储多个标记。


>每个 GameplayTag 都由一个或多个名称组成,这些名称构成了一个层次结构,类似于文件系统中的文件路径。例如,"Character.Player.Hero" 可以表示一个角色的玩家英雄标记,其中 "Character" 是顶层标记,"Player" 是其子标记,"Hero" 是 "Player" 的子标记。
___________________________________________________________________________________________


#### GameplayTags 的主要功能可以分为两个方面:标记管理和标记操作。

- 标记管理:


- 注册和创建: 游戏开发者可以在游戏启动时注册和创建需要的标记。通过 FGameplayTag::RequestGameplayTag() 函数可以创建一个 GameplayTag。

- 层次结构: 标记之间可以建立层次关系,形成树状结构,方便对标记进行组织和管理。


- 元数据: 每个标记可以关联一些元数据,比如描述信息、父标记等。


- 标记操作:


- 查询和比较: 可以通过 FGameplayTagContainer 类提供的函数来查询标记是否存在于容器中,或者进行标记之间的比较操作。
	- 标记集合操作: 可以对多个标记进行集合操作,包括并集、交集、差集等,以便于进行标记的组合和过滤。
	- 标记解析: 可以将字符串形式的标记路径解析成 GameplayTag,或者将 GameplayTag 转换成字符串形式的路径。

- 两个标签可以进行精确比较,甚至部分比较。也许它们只共享相同的根标签名称,这在代码中可能很重要。
___________________________________________________________________________________________

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/287284_620511.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/125188_983981.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/444596_69816.png?raw=true)
___________________________________________________________________________________________


### 创建GameplayTags几种方法



#### 第一种 在编辑器的 项目设置 中, 添加GamplayTag标签

###### 在编辑器的 项目设置 中, 添加GamplayTag标签

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/476031_313668.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/138446_208989.png?raw=true)
- 添加后 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/471140_480224.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/391491_235380.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/389900_2036.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/524022_987358.png?raw=true)
___________________________________________________________________________________________


####  第二种 使用 表格

###### BP 下创建 AbilitySystem 文件夹

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/860045_9652.png?raw=true)
###### AbilitySystem 文件夹下创建 GameplayTags 文件夹

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/493953_526254.png?raw=true)
###### GameplayTags 文件夹中,添加数据表格

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/491467_549912.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/163058_452606.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/844642_413516.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/518630_953758.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/948103_867766.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/354690_780860.png?raw=true)

___________________________________________________________________________________________


###### 项目设置中使用自建的GamplayTags表格

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/851600_837116.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/730970_758902.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/631821_561960.png?raw=true)
___________________________________________________________________________________________


#### 在项目中打开配置文件

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/900911_484275.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/395591_569251.png?raw=true)
___________________________________________________________________________________________


### 给物体添加标签, 理解用的测试 (如果操作,记得撤销操作)

#### 理解用的测试 (如果操作,记得撤销操作)
##### 给物体添加标签
###### 比如,在加血的水晶上加一个标签

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/816784_408608.png?raw=true)
___________________________________________________________________________________________


###### 拾取水晶
- 未拾取时,身上没有Tag标签 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/971241_669442.png?raw=true)
- 拾取后,水晶持续时间内身上会持有这个刚设置的标签,持续时间结束后,该标签会被移除 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/576545_970822.png?raw=true)
___________________________________________________________________________________________


###### 帮助理解: 修改堆叠测试
- 修改堆叠计数为3,一次吃三个水晶,身上也只有一个Tag

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/717493_797127.png?raw=true)
- 如果取消了堆叠,一次吃三个水晶,身上有3个Tag

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/841468_428019.png?raw=true)

- 拾取前 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/555951_893254.png?raw=true)
- 拾取后 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/235327_422617.png?raw=true)
___________________________________________________________________________________________


##### 只有有持续时间的,添加 GE下的Component下的Target Tags Gameplay Effect Component 下的Tag标签 才有意义 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/985213_11926.png?raw=true)

___________________________________________________________________________________________


##### 如果是瞬时生效的需要Tag,需要加资产标签AssetTag,先了解
___________________________________________________________________________________________


#### RPC参考这张图 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_011/936265_104861.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#Go主菜单)
___________________________________________________________________________________________