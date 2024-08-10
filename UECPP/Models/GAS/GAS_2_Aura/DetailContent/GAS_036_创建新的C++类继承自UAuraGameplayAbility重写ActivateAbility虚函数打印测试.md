___________________________________________________________________________________________

###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________

# GAS_036_创建新的C++类继承自UAuraGameplayAbility重写ActivateAbility虚函数打印测试

___________________________________________________________________________________________


# 目录
- [GAS 036 创建新的C++类继承自UAuraGameplayAbility重写ActivateAbility虚函数打印测试](#gas-036-创建新的c类继承自uauragameplayability重写activateability虚函数打印测试)
- [目录](#目录)
    - [视频链接](#视频链接)
      - [【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）\_哔哩哔哩】 https://b23.tv/XvDjaI1](#ai中字虚幻5c教程使用gas制作rpg游戏一_哔哩哔哩-httpsb23tvxvdjai1)
    - [创建新的C++类继承自 `UAuraGameplayAbility`](#创建新的c类继承自-uauragameplayability)
    - [`UAuraProjectileSpell` 中,重写基类中 `ActivateAbility` 这个虚函数](#uauraprojectilespell-中重写基类中-activateability-这个虚函数)
      - [头文件](#头文件)
      - [源文件](#源文件)
    - [创建`UAuraProjectileSpell`的蓝图派生类 *GA\_FireBolt*](#创建uauraprojectilespell的蓝图派生类-ga_firebolt)
    - [在角色 *BP\_Aura* 中配置,才能生效](#在角色-bp_aura-中配置才能生效)
    - [此时测试结果, 蓝图先打印,C++后打印](#此时测试结果-蓝图先打印c后打印)


___________________________________________________________________________________________


### 视频链接
___________________________________________________________________________________________


#### 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）_哔哩哔哩】 [https://b23.tv/XvDjaI1]("https://b23.tv/XvDjaI1")
___________________________________________________________________________________________


### 创建新的C++类继承自 `UAuraGameplayAbility`

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_036/514965_783.png?raw=true)
___________________________________________________________________________________________


### `UAuraProjectileSpell` 中,重写基类中 `ActivateAbility` 这个虚函数
___________________________________________________________________________________________


#### 头文件

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_036/75614_580836.png?raw=true)
___________________________________________________________________________________________


#### 源文件

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_036/343261_406875.png?raw=true)
___________________________________________________________________________________________


### 创建`UAuraProjectileSpell`的蓝图派生类 *GA_FireBolt*

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_036/936274_277420.png?raw=true)
     
![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_036/372015_236754.png?raw=true)
___________________________________________________________________________________________


### 在角色 *BP_Aura* 中配置,才能生效

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_036/979458_823078.png?raw=true)
___________________________________________________________________________________________


### 此时测试结果, 蓝图先打印,C++后打印  
![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_036/227932_894669.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#Go主菜单)
___________________________________________________________________________________________