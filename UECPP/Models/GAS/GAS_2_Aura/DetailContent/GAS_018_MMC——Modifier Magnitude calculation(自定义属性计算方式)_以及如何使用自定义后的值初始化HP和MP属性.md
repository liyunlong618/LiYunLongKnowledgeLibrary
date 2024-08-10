___________________________________________________________________________________________

###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________

# GAS_018_MMC——Modifier Magnitude calculation(自定义属性计算方式)_以及如何使用自定义后的值初始化HP和MP属性
___________________________________________________________________________________________
## 处理关键点
1. 自定义属性计算方式需要创建类`GameplayModMagnitudecalculation`
   - //步骤一:需要依赖的属性 要创建`FGameplayEffectAttributecaptureDefinition`类变量 构造中,给变量配置参数
   - //步骤二:重写虚函数`CalculateBaseMagnitude`并调用核心处理API`GetCapturedAttributeMagnitude`为变量赋值,然后通过`FGameplayEffectSpec`拿到角色数据,计算并返回
   - //步骤三:GE中配置自定义计算方式
___________________________________________________________________________________________


# 目录
- [GAS 018 MMC——Modifier Magnitude calculation(自定义属性计算方式);以及如何使用自定义后的值初始化HP/MP属性](#gas-018-mmcmodifier-magnitude-calculation自定义属性计算方式以及如何使用自定义后的值初始化hpmp属性)
	- [处理关键点](#处理关键点)
	- [目录](#目录)
		- [下一步任务](#下一步任务)
		- [创建 GameplayModMagnitudeCalculation 类C++文件（\_ 游戏修正幅度计算）又叫MMC](#创建-gameplaymodmagnitudecalculation-类c文件_-游戏修正幅度计算又叫mmc)
		- [UMMC\_MaxHealth 中创建构造](#ummc_maxhealth-中创建构造)
		- [修改 *GE\_AuraSecondaryAttributes* 次要属性中的MaxHP的计算方式](#修改-ge_aurasecondaryattributes-次要属性中的maxhp的计算方式)
		- [这里处理之前的遗漏](#这里处理之前的遗漏)
			- [1.Source为空,因为 `AAuraCharacterBase` 中初始化属性(应用GE)时并没有指定Source](#1source为空因为-aauracharacterbase-中初始化属性应用ge时并没有指定source)
			- [2.`PS`中`Level`没有给默认为1所以初始等级为0](#2ps中level没有给默认为1所以初始等级为0)
		- [测试结果](#测试结果)
			- [所以`MaxHP=80+9*1*15=215 `](#所以maxhp809115215-)
		- [小测试:使用自定义属性计算方式法力最大值](#小测试使用自定义属性计算方式法力最大值)
			- [自己尝试一下](#自己尝试一下)
		- [测试结果](#测试结果-1)
			- [所以`MaxMP=90+17*1*25=515`](#所以maxmp9017125515)
			- [当然我这个数值设定不一定合理,这个随意](#当然我这个数值设定不一定合理这个随意)
		- [使用自定义后的值初始化HP/MP属性](#使用自定义后的值初始化hpmp属性)
			- [不用在 UAuraAttributeSet 构造中初始化HP/MP了](#不用在-uauraattributeset-构造中初始化hpmp了)
		- [小测试:初始化HP/MP使用最大值, 提示:使用GE](#小测试初始化hpmp使用最大值-提示使用ge)
			- [自己尝试一下](#自己尝试一下-1)



___________________________________________________________________________________________



### 下一步任务

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/783593_966830.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/61766_180318.png?raw=true)
___________________________________________________________________________________________


### 创建 GameplayModMagnitudeCalculation 类C++文件（_ 游戏修正幅度计算）又叫MMC

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/918871_880172.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/779229_219152.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/886762_90298.png?raw=true)
___________________________________________________________________________________________


### UMMC_MaxHealth 中创建构造

重写 `CalculateBaseMagnitude` 虚函数,并创建一个 `FGameplayEffectAttributeCaptureDefinition` 类型的变量（这个类型是一个集合信息的结构体）

&emsp;

&emsp;

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/415115_796974.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/535795_916183.png?raw=true)

+ `头文件`中：
```cpp
// Copyright Druid Mechanics
#pragma once
#include "CoreMinimal.h"
#include "GameplayModMagnitudeCalculation.h"
#include "MMC_MaxHealth.generated.h"
DECLARE_LOG_CATEGORY_CLASS(MYLOG_UMMC_MaxHealth,Log,All)

UCLASS()
class DIABLOLIKE_API UMMC_MaxHealth : public UGameplayModMagnitudeCalculation
{
	GENERATED_BODY()	
public:
	UMMC_MaxHealth();
	virtual float CalculateBaseMagnitude_Implementation(const FGameplayEffectSpec& Spec) const override;
protected:
	FGameplayEffectAttributeCaptureDefinition VigorDef;
};

```

&emsp;

+ `源文件`中：
```cpp
// Copyright Druid Mechanics


#include "AbilitySystem/MMC/MMC_MaxHealth.h"

#include "AbilitySystem/AuraAttributeSet.h"
#include "Interactrion/CombatInterface.h"

UMMC_MaxHealth::UMMC_MaxHealth()
{
	VigorDef.AttributeToCapture = UAuraAttributeSet::GetVigorAttribute();
	VigorDef.AttributeSource = EGameplayEffectAttributeCaptureSource::Target;
	VigorDef.bSnapshot = false;
	//核心是需要将这个属性先添加到捕获的数组
	//此数组在 父类 UGameplayModMagnitudeCalculation 的父类 UGameplayEffectCalculation 中
	RelevantAttributesToCapture.Add(VigorDef);
}

float UMMC_MaxHealth::CalculateBaseMagnitude_Implementation(const FGameplayEffectSpec& Spec) const
{
	//return Super::CalculateBaseMagnitude_Implementation(Spec);

	//先获取Source和Target的Tag
	const FGameplayTagContainer* SourceTags = Spec.CapturedSourceTags.GetAggregatedTags();
	const FGameplayTagContainer* TargetTags = Spec.CapturedTargetTags.GetAggregatedTags();

	//需要传入Source和Target	这两个的Tag
	FAggregatorEvaluateParameters EvaluateParameters;
	EvaluateParameters.SourceTags = SourceTags;
	EvaluateParameters.TargetTags = TargetTags;
	
	//创建一个Float接一下属性
	float Vigor;
	//调用这个API获取属性值
	GetCapturedAttributeMagnitude(VigorDef,Spec,EvaluateParameters,Vigor);

	//限制最小值为0
	Vigor = FMath::Max<float>(Vigor,0.f);

	//看目标是否实现了接口类
	const TScriptInterface<ICombatInterface> SourceActor = Spec.GetContext().GetSourceObject();
	if (SourceActor != nullptr)
	{
		//拿到目标等级
		const int32 PlayerLevel = SourceActor.GetInterface()->GetPlayerLevel();

		//自定义计算方法
		const float Value = 80.f + Vigor * PlayerLevel * 15.f;
		
		return Value;
	}
	else
	{
		UE_LOG(MYLOG_UMMC_MaxHealth, Warning, TEXT("SourceActor为空	return 0.f	！！！"))
	}
	return 0.f;
}

```


___________________________________________________________________________________________


### 修改 *GE_AuraSecondaryAttributes* 次要属性中的MaxHP的计算方式

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/329204_263916.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/845159_788059.png?raw=true)
___________________________________________________________________________________________


### 这里处理之前的遗漏
___________________________________________________________________________________________


#### 1.Source为空,因为 `AAuraCharacterBase` 中初始化属性(应用GE)时并没有指定Source

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/273965_855642.png?raw=true)
___________________________________________________________________________________________


#### 2.`PS`中`Level`没有给默认为1所以初始等级为0

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/21499_80346.png?raw=true)
___________________________________________________________________________________________


### 测试结果
___________________________________________________________________________________________


#### 所以`MaxHP=80+9*1*15=215 `

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/951979_960659.png?raw=true)

```CPP
		//自定义计算方法
		const float Value = 80.f + Vigor * PlayerLevel * 15.f;
```



![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/753239_698218.png?raw=true)
___________________________________________________________________________________________


### 小测试:使用自定义属性计算方式法力最大值 
![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/264761_928466.png?raw=true)
___________________________________________________________________________________________

#### 自己尝试一下

`UMMC_MaxMana`中

&emsp;

+ `头文件`中：
```cpp
// Copyright Druid Mechanics
#pragma once
#include "CoreMinimal.h"
#include "GameplayModMagnitudeCalculation.h"
#include "MMC_MaxMana.generated.h"

DECLARE_LOG_CATEGORY_CLASS(MYLOG_UUMMC_MaxMana,Log,All);

UCLASS()
class DIABLOLIKE_API UMMC_MaxMana : public UGameplayModMagnitudeCalculation
{
	GENERATED_BODY()
public:
	UMMC_MaxMana();
	virtual float CalculateBaseMagnitude_Implementation(const FGameplayEffectSpec& Spec) const override;
protected:
	FGameplayEffectAttributeCaptureDefinition IntelligenceDef;
};

```

&emsp;

+ `源文件`中：
```cpp
// Copyright Druid Mechanics

#include "AbilitySystem/MMC/MMC_MaxMana.h"
#include "AbilitySystem/AuraAttributeSet.h"
#include "Interactrion/CombatInterface.h"

UMMC_MaxMana::UMMC_MaxMana()
{
	IntelligenceDef.AttributeToCapture = UAuraAttributeSet::GetIntelligenceAttribute();
	IntelligenceDef.AttributeSource = EGameplayEffectAttributeCaptureSource::Target;
	IntelligenceDef.bSnapshot = false;
	RelevantAttributesToCapture.Add(IntelligenceDef);
}

float UMMC_MaxMana::CalculateBaseMagnitude_Implementation(const FGameplayEffectSpec& Spec) const
{
	//return Super::CalculateBaseMagnitude_Implementation(Spec);
	const FGameplayTagContainer* SourceTags = Spec.CapturedSourceTags.GetAggregatedTags();
	const FGameplayTagContainer* TargetTags = Spec.CapturedTargetTags.GetAggregatedTags();
	FAggregatorEvaluateParameters EvaluationParameters;
	EvaluationParameters.SourceTags = SourceTags;
	EvaluationParameters.TargetTags = TargetTags;
	float Intelligence;
	GetCapturedAttributeMagnitude(IntelligenceDef, Spec, EvaluationParameters, Intelligence);
	Intelligence = FMath::Max(Intelligence, 0.f);
	const TScriptInterface<ICombatInterface> SourceActor = Spec.GetContext().GetSourceObject();
	if (SourceActor != nullptr)
	{
		const int32 PlayerLevel = SourceActor.GetInterface()->GetPlayerLevel();
		const float MaxMana = 50.f +2.5f* Intelligence + PlayerLevel * 15.f;
		UE_LOG(MYLOG_UUMMC_MaxMana, Log, TEXT("MaxMana:%f"), MaxMana)
		return MaxMana;
	}
	else
	{
		UE_LOG(MYLOG_UUMMC_MaxMana, Warning, TEXT("SourceActor == nullptr"))
	}
	return 0.f;
}

```

&emsp;

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/221407_939573.png?raw=true)
___________________________________________________________________________________________


### 测试结果
___________________________________________________________________________________________


#### 所以`MaxMP=90+17*1*25=515` 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/513529_21156.png?raw=true)
___________________________________________________________________________________________


#### 当然我这个数值设定不一定合理,这个随意 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/371823_625409.png?raw=true)
___________________________________________________________________________________________


### 使用自定义后的值初始化HP/MP属性
___________________________________________________________________________________________


#### 不用在 UAuraAttributeSet 构造中初始化HP/MP了

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/725722_545360.png?raw=true)
___________________________________________________________________________________________


### 小测试:初始化HP/MP使用最大值, 提示:使用GE 
![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/200484_902910.png?raw=true)
___________________________________________________________________________________________


#### 自己尝试一下

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/439807_232906.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/246098_838931.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/679826_404457.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_018/99329_535508.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#Go主菜单)
___________________________________________________________________________________________