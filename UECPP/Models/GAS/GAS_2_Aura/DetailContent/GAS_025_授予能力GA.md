___________________________________________________________________________________________

###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________

# GAS_025_授予能力GA
___________________________________________________________________________________________
## 处理关键点
1. 只有服务器才能赋予技能
2. 学习技能时,先使用GA的Class创建FGameplayabilitySpec技能规范,然后调用API:`GiveAbilityAndActivateOnce`(这里传入技能规范)才能学习
___________________________________________________________________________________________


# 目录
- [GAS 025 授予能力GA](#gas-025-授予能力ga)
  - [处理关键点](#处理关键点)
- [目录](#目录)
    - [创建GA文件](#创建ga文件)
    - [AAuraCharacterBase 中创建 存放 技能GA类的数组,并创建需要学习技能时调用的函数 `AddCharacterAbilities()`](#aauracharacterbase-中创建-存放-技能ga类的数组并创建需要学习技能时调用的函数-addcharacterabilities)
    - [UAuraAbilitySystemComponent 中,创建 调用时 传入要学的GA类 数组 （ const引用 ）函数,并学习技能](#uauraabilitysystemcomponent-中创建-调用时-传入要学的ga类-数组--const引用-函数并学习技能)
    - [AAuraCharacter 中,当角色PossessedBy时,调用基类中的学习技能的函数 `AddCharacterAbilities()`](#aauracharacter-中当角色possessedby时调用基类中的学习技能的函数-addcharacterabilities)
    - [创建GA文件夹,并创建 测试用GA类继承自UAuraGameplayAbility](#创建ga文件夹并创建-测试用ga类继承自uauragameplayability)
    - [使用测试的GA 测试](#使用测试的ga-测试)
      - [测试结果](#测试结果)


___________________________________________________________________________________________



### 创建GA文件


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/816207_659845.png?raw=true)


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/964889_58254.png?raw=true)
___________________________________________________________________________________________


### AAuraCharacterBase 中创建 存放 技能GA类的数组,并创建需要学习技能时调用的函数 `AddCharacterAbilities()`


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/622868_138872.png?raw=true)


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/479469_965246.png?raw=true)
___________________________________________________________________________________________


### UAuraAbilitySystemComponent 中,创建 调用时 传入要学的GA类 数组 （ const引用 ）函数,并学习技能


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/112254_233365.png?raw=true)


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/978582_586363.png?raw=true)
___________________________________________________________________________________________


### AAuraCharacter 中,当角色PossessedBy时,调用基类中的学习技能的函数 `AddCharacterAbilities()`


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/668086_400015.png?raw=true)
___________________________________________________________________________________________


### 创建GA文件夹,并创建 测试用GA类继承自UAuraGameplayAbility


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/558686_802729.png?raw=true)


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/960664_574075.png?raw=true)


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/805801_892780.png?raw=true)
___________________________________________________________________________________________


### 使用测试的GA 测试


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/552141_562667.png?raw=true)


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/177369_109541.png?raw=true)
___________________________________________________________________________________________


#### 测试结果  

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_025/906951_983114.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#Go主菜单)
___________________________________________________________________________________________