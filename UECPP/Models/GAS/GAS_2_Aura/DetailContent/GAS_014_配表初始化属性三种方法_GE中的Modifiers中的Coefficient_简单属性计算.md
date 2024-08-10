___________________________________________________________________________________________

###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________

# GAS_014_配表初始化属性三种方法_GE中的Modifiers中的Coefficient_简单属性计算
___________________________________________________________________________________________
## 处理关键点
1. 初始化属性的三种方法
___________________________________________________________________________________________


# 目录
- [GAS 014 配表 初始化属性:GE中的Modifiers中的Coefficient（简单属性计算）](#gas-014-配表-初始化属性ge中的modifiers中的coefficient简单属性计算)
	- [处理关键点](#处理关键点)
	- [目录](#目录)
		- [初始化属性的三种方法](#初始化属性的三种方法)
			- [方法一 :在构造中赋值](#方法一-在构造中赋值)
			- [方法二 :配表 初始化属性](#方法二-配表-初始化属性)
				- [创建BP的PS并配置](#创建bp的ps并配置)
				- [`UAuraAttributeSet` 中添加人物主要属性:`力量` `智力` `坚韧` `活力`](#uauraattributeset-中添加人物主要属性力量-智力-坚韧-活力)
				- [`AAuraPlayerState` 中设置`ASC组件`为 蓝图可读,这样就能配表了](#aauraplayerstate-中设置asc组件为-蓝图可读这样就能配表了)
				- [创建并配置表格](#创建并配置表格)
				- [*BP\_AuraPlayerState*中配置表格](#bp_auraplayerstate中配置表格)
				- [运行游戏,初始化属性成功](#运行游戏初始化属性成功)
				- [配表 虽然方便,但是缺点也很明显,这里只能起到初始化的作用,最大最小值无效,不如别的地方功能性更强](#配表-虽然方便但是缺点也很明显这里只能起到初始化的作用最大最小值无效不如别的地方功能性更强)
			- [移除配表 配表只做了解](#移除配表-配表只做了解)
				- [看到属性归零](#看到属性归零)
			- [方法三 :使用GE初始化属性](#方法三-使用ge初始化属性)
				- [`AAuraCharacterBase` 中,增加蓝图可配置的初始化属性的GE类,和初始化调用GE的函数](#aauracharacterbase-中增加蓝图可配置的初始化属性的ge类和初始化调用ge的函数)
					- [根据GE类,创建`FGameplayEffectSpecHandle`并应用到自身](#根据ge类创建fgameplayeffectspechandle并应用到自身)
				- [`AAuraCharacter` 的 `InitAbilityActorInfo()` 函数中调用](#aauracharacter-的-initabilityactorinfo-函数中调用)
				- [创建文件夹](#创建文件夹)
				- [`AbilitySystem \ GameplayEffects \ PrimaryAttributes`文件夹下创建初始化用的GE文件](#abilitysystem--gameplayeffects--primaryattributes文件夹下创建初始化用的ge文件)
				- [别忘了给*BP\_Aura* 配置`DefaultPrimaryAttributes`(使用初始化用的GE   *GE\_AuraPrimaryAttributes*)](#别忘了给bp_aura-配置defaultprimaryattributes使用初始化用的ge---ge_auraprimaryattributes)
		- [帮助理解的小案例](#帮助理解的小案例)
				- [创建一个Actor 拥有组件`BoxCollision` `BeginOverlap`时触发GE 根据角色属性触发\_HP的逻辑](#创建一个actor-拥有组件boxcollision-beginoverlap时触发ge-根据角色属性触发_hp的逻辑)
					- [新建文件夹/Actor/GE](#新建文件夹actorge)
					- [设置GE](#设置ge)
				- [结果](#结果)
				- [属性](#属性)
		- [GE中的`Modifiers`（简单属性计算）](#ge中的modifiers简单属性计算)
				- [如果有三个`Modifier`,分别根据人物`活力``力量``坚韧`触发加血的GE逻辑](#如果有三个modifier分别根据人物活力力量坚韧触发加血的ge逻辑)
				- [严格按照下标的顺序进行 逻辑运算](#严格按照下标的顺序进行-逻辑运算)
		- [GE 中的 `Modifiers` 中的 `Coefficient`](#ge-中的-modifiers-中的-coefficient)


___________________________________________________________________________________________


### 初始化属性的三种方法
___________________________________________________________________________________________


#### 方法一 :在构造中赋值

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/259693_386607.png?raw=true)

```CPP
UAuraAttributeSet::UAuraAttributeSet()
{
	InitHP(50.f);
	InitMaxHP(100.f);
	InitMP(1.f);
	InitMaxMP(50.f);
}
```



___________________________________________________________________________________________


#### 方法二 :配表 初始化属性
___________________________________________________________________________________________


##### 创建BP的PS并配置

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/735085_113350.png?raw=true)
___________________________________________________________________________________________


##### `UAuraAttributeSet` 中添加人物主要属性:`力量` `智力` `坚韧` `活力`
___________________________________________________________________________________________


- 头文件

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/236964_145056.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/800934_653335.png?raw=true)

- 下面我直接把我的`UAuraAttributeSet`头文件放上来&emsp;

```cpp
#pragma once

#include "CoreMinimal.h"
#include "AttributeSet.h"
#include "AbilitySystemComponent.h"
#include "AuraAttributeSet.generated.h"
DECLARE_LOG_CATEGORY_CLASS(MyLog_UAuraAttributeSet,Log,All);

#define ATTRIBUTE_ACCESSORS(ClassName, PropertyName) \
GAMEPLAYATTRIBUTE_PROPERTY_GETTER(ClassName, PropertyName) \
GAMEPLAYATTRIBUTE_VALUE_GETTER(PropertyName) \
GAMEPLAYATTRIBUTE_VALUE_SETTER(PropertyName) \
GAMEPLAYATTRIBUTE_VALUE_INITTER(PropertyName)

USTRUCT()
struct FEffectProperties
{
	GENERATED_BODY()
	FEffectProperties(): SourceASC(nullptr), SourceAvatarActor(nullptr), SourceController(nullptr),
	                     SourceCharacter(nullptr),
	                     TargetASC(nullptr),
	                     TargetAvatarActor(nullptr),
	                     TargetController(nullptr),
	                     TargetCharacter(nullptr)
	{
	}
    
	UPROPERTY()
	FGameplayEffectContextHandle EffectContextHandle;
	
	UPROPERTY()
	UAbilitySystemComponent* SourceASC;
	UPROPERTY()
	AActor* SourceAvatarActor;
	UPROPERTY()
	AController* SourceController;
	UPROPERTY()
	ACharacter* SourceCharacter;

	UPROPERTY()
	UAbilitySystemComponent* TargetASC;
	UPROPERTY()
	AActor* TargetAvatarActor;
	UPROPERTY()
	AController* TargetController;
	UPROPERTY()
	ACharacter* TargetCharacter;
};
UCLASS()
class DIABLOLIKE_API UAuraAttributeSet : public UAttributeSet
{
	GENERATED_BODY()
public:
	UAuraAttributeSet();
	virtual void GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const override;
	virtual void PreAttributeChange(const FGameplayAttribute& Attribute, float& NewValue) override;
	virtual void PostGameplayEffectExecute(const FGameplayEffectModCallbackData& Data) override;

	//主要属性
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_Strength, Category="Primary|Attribute")
	FGameplayAttributeData Strength;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, Strength);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_Intelligence, Category="Primary|Attribute")
	FGameplayAttributeData Intelligence;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, Intelligence);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_Resilience, Category="Primary|Attribute")
	FGameplayAttributeData Resilience;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, Resilience);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_Vigor, Category="Primary|Attribute")
	FGameplayAttributeData Vigor;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, Vigor);
	//次要属性
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_Armor, Category="Secondary|Attribute")
	FGameplayAttributeData Armor;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, Armor);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_ArmorPenetration, Category="Secondary|Attribute")
	FGameplayAttributeData ArmorPenetration;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, ArmorPenetration);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_BlockChance, Category="Secondary|Attribute")
	FGameplayAttributeData BlockChance;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, BlockChance);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_CriticalHitChance, Category="Secondary|Attribute")
	FGameplayAttributeData CriticalHitChance;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, CriticalHitChance);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_CriticalHitDamage, Category="Secondary|Attribute")
	FGameplayAttributeData CriticalHitDamage;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, CriticalHitDamage);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_CriticalHitResistance, Category="Secondary|Attribute")
	FGameplayAttributeData CriticalHitResistance;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, CriticalHitResistance);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_HealthRegeneration, Category="Secondary|Attribute")
	FGameplayAttributeData HealthRegeneration;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, HealthRegeneration);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_ManaRegeneration, Category="Secondary|Attribute")
	FGameplayAttributeData ManaRegeneration;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, ManaRegeneration);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_MaxHP, Category="Vita|Attribute")
	FGameplayAttributeData MaxHP;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, MaxHP);
	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_MaxMP, Category="Vita|Attribute")
	FGameplayAttributeData MaxMP;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, MaxMP);

	UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_HP, Category="Vita|Attribute")
	FGameplayAttributeData HP;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, HP);
    UPROPERTY(BlueprintReadOnly, ReplicatedUsing = OnRep_MP, Category="Vita|Attribute")
	FGameplayAttributeData MP;
	ATTRIBUTE_ACCESSORS(UAuraAttributeSet, MP);

	UFUNCTION()
	void OnRep_HP(const FGameplayAttributeData& OldHP);
	UFUNCTION()
	void OnRep_MP(const FGameplayAttributeData& OldMP);
    
	//主要属性
	UFUNCTION()
	void OnRep_Strength(const FGameplayAttributeData& OldStrength);
	UFUNCTION()
	void OnRep_Intelligence(const FGameplayAttributeData& OldIntelligence);
	UFUNCTION()
	void OnRep_Resilience(const FGameplayAttributeData& OldResilience);
	UFUNCTION()
	void OnRep_Vigor(const FGameplayAttributeData& OldVigor);
	//次要属性
	UFUNCTION()
	void OnRep_Armor(const FGameplayAttributeData& OldArmor);
	UFUNCTION()
	void OnRep_ArmorPenetration(const FGameplayAttributeData& OldArmorPenetration);
	UFUNCTION()
	void OnRep_BlockChance(const FGameplayAttributeData& OldBlockChance);
	UFUNCTION()
	void OnRep_CriticalHitChance(const FGameplayAttributeData& OldCriticalHitChance);
	UFUNCTION()
	void OnRep_CriticalHitDamage(const FGameplayAttributeData& OldCriticalHitDamage);
	UFUNCTION()
	void OnRep_CriticalHitResistance(const FGameplayAttributeData& OldCriticalHitResistance);
	UFUNCTION()
	void OnRep_HealthRegeneration(const FGameplayAttributeData& OldHealthRegeneration);
	UFUNCTION()
	void OnRep_ManaRegeneration(const FGameplayAttributeData& OldManaRegeneration);
	UFUNCTION()
	void OnRep_MaxHP(const FGameplayAttributeData& OldMaxHP);
	UFUNCTION()
	void OnRep_MaxMP(const FGameplayAttributeData& OldMaxMP);
private:
	void SetEffectProperties(const FGameplayEffectModCallbackData& Data, FEffectProperties& Props) const ;
};
```

&emsp;

___________________________________________________________________________________________


- 源文件

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/210478_889833.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/973321_582084.png?raw=true)

- 下面我直接把我的`UAuraAttributeSet`源文件放上来

```CPP
// Fill out your copyright notice in the Description page of Project Settings.


#include "AbilitySystem/AuraAttributeSet.h"

#include "AbilitySystemBlueprintLibrary.h"
#include "AbilitySystemComponent.h"
#include "GameplayEffectExtension.h"
#include "GameFramework/Character.h"
#include "Net/UnrealNetwork.h"

UAuraAttributeSet::UAuraAttributeSet()
{
	InitHP(50.f);
	InitMP(1.f);
	//InitMaxHP(100.f);
	//InitMaxMP(50.f);
}

void UAuraAttributeSet::GetLifetimeReplicatedProps(TArray<FLifetimeProperty>& OutLifetimeProps) const
{
	Super::GetLifetimeReplicatedProps(OutLifetimeProps);
	
	//此函数在UnrealNetwork.cpp中  需要提供的参数(哪个类中,哪个参数,同步条件,什么时候同步数据)
	//同步方式常用的还有 COND_Custom 网络优化时可能遇到		例如:假如这个数据很大时 比如玩家附近的所有数据 这个可以自定义为 相机视野范围内的东西同步 条件可以写在 COND_Custom 中InitMP(1.f);
    
	//主要属性
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,Strength,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,Intelligence,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,Resilience,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,Vigor,COND_None,REPNOTIFY_Always);
	//次要属性
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,Armor,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,ArmorPenetration,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,BlockChance,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,CriticalHitChance,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,CriticalHitDamage,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,CriticalHitResistance,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,HealthRegeneration,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,ManaRegeneration,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,MaxHP,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,MaxMP,COND_None,REPNOTIFY_Always);
	//角色HP/MP
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,HP,COND_None,REPNOTIFY_Always);
	DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet,MP,COND_None,REPNOTIFY_Always);
}
		UE_LOG(MyLog_UAuraAttributeSet, Log, TEXT("TargetController : %s"),*Props.TargetController->GetName())
		UE_LOG(MyLog_UAuraAttributeSet, Log, TEXT("TargetCharacter : %s"),*Props.TargetCharacter->GetName())
		UE_LOG(MyLog_UAuraAttributeSet, Log, TEXT("TargetASC : %s"),*Props.TargetASC->GetName())
	}
	
}

void UAuraAttributeSet::PostGameplayEffectExecute(const FGameplayEffectModCallbackData& Data)
{
	Super::PostGameplayEffectExecute(Data);

	FEffectProperties Props;
	SetEffectProperties(Data,Props);
	
	//现在必须在这里修改属性了
	if (Data.EvaluatedData.Attribute == GetHPAttribute())
	{
		SetHP(FMath::Clamp(GetHP(),0.f,GetMaxHP()));
		UE_LOG(MyLog_UAuraAttributeSet, Log, TEXT("HP:			%f"),GetHP())
		UE_LOG(MyLog_UAuraAttributeSet, Log, TEXT("Magnitude(HP变化量):	%f"),Data.EvaluatedData.Magnitude)
	}
	if (Data.EvaluatedData.Attribute == GetMPAttribute())
	{
		SetMP(FMath::Clamp(GetMP(),0.f,GetMaxMP()));
		UE_LOG(MyLog_UAuraAttributeSet, Log, TEXT("MP:			%f"),GetMP())
		UE_LOG(MyLog_UAuraAttributeSet, Log, TEXT("Magnitude(MP变化量):	%f"),Data.EvaluatedData.Magnitude)
	}
}

void UAuraAttributeSet::OnRep_HP(const FGameplayAttributeData& OldHP)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet, HP, OldHP);
}
void UAuraAttributeSet::OnRep_MP(const FGameplayAttributeData& OldMP)
{
    GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet, MP, OldMP);
}
void UAuraAttributeSet::OnRep_Strength(const FGameplayAttributeData& OldStrength)
{
    	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Strength,OldStrength);
}

void UAuraAttributeSet::OnRep_Intelligence(const FGameplayAttributeData& OldIntelligence)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Intelligence,OldIntelligence);
}

void UAuraAttributeSet::OnRep_Resilience(const FGameplayAttributeData& OldResilience)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Resilience,OldResilience);
}

void UAuraAttributeSet::OnRep_Vigor(const FGameplayAttributeData& OldVigor)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Vigor,OldVigor);
}

void UAuraAttributeSet::OnRep_Armor(const FGameplayAttributeData& OldArmor)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Vigor,OldArmor);
}

void UAuraAttributeSet::OnRep_ArmorPenetration(const FGameplayAttributeData& OldArmorPenetration)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Vigor,OldArmorPenetration);
}

void UAuraAttributeSet::OnRep_BlockChance(const FGameplayAttributeData& OldBlockChance)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Vigor,OldBlockChance);
}

void UAuraAttributeSet::OnRep_CriticalHitChance(const FGameplayAttributeData& OldCriticalHitChance)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Vigor,OldCriticalHitChance);
}

void UAuraAttributeSet::OnRep_CriticalHitDamage(const FGameplayAttributeData& OldCriticalHitDamage)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Vigor,OldCriticalHitDamage);
}

void UAuraAttributeSet::OnRep_CriticalHitResistance(const FGameplayAttributeData& OldCriticalHitResistance)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Vigor,OldCriticalHitResistance);
}

void UAuraAttributeSet::OnRep_HealthRegeneration(const FGameplayAttributeData& OldHealthRegeneration)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Vigor,OldHealthRegeneration);
}

void UAuraAttributeSet::OnRep_ManaRegeneration(const FGameplayAttributeData& OldManaRegeneration)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet,Vigor,OldManaRegeneration);
}

void UAuraAttributeSet::OnRep_MaxHP(const FGameplayAttributeData& OldMaxHP)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet, MaxHP, OldMaxHP);
}

void UAuraAttributeSet::OnRep_MaxMP(const FGameplayAttributeData& OldMaxMP)
{
	GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet, MaxMP, OldMaxMP);
}
```



___________________________________________________________________________________________


##### `AAuraPlayerState` 中设置`ASC组件`为 蓝图可读,这样就能配表了

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/728098_869570.png?raw=true)
___________________________________________________________________________________________


##### 创建并配置表格

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/133291_384936.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/255623_609942.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/528734_139988.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/66543_782239.png?raw=true)
___________________________________________________________________________________________


##### *BP_AuraPlayerState*中配置表格

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/809545_620944.png?raw=true)
___________________________________________________________________________________________


##### 运行游戏,初始化属性成功 

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/823609_309359.png?raw=true)
___________________________________________________________________________________________


##### 配表 虽然方便,但是缺点也很明显,这里只能起到初始化的作用,最大最小值无效,不如别的地方功能性更强
___________________________________________________________________________________________


####  移除配表 配表只做了解

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/52097_785648.png?raw=true)
___________________________________________________________________________________________


##### 看到属性归零

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/298821_463392.png?raw=true)
___________________________________________________________________________________________


#### 方法三 :使用GE初始化属性


##### `AAuraCharacterBase` 中,增加蓝图可配置的初始化属性的GE类,和初始化调用GE的函数

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/251747_164999.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/454401_240645.png?raw=true)

&emsp;

+ `头文件`中：

```CPP
class UGameplayEffect;
```


```cpp
	//初始化 主要属性 用的GE
	UPROPERTY(BlueprintReadOnly,EditAnywhere,Category="Attributes")
	TSubclassOf<UGameplayEffect> DefaultPrimaryAttributes;

	//调用这个函数  使用上面的初始化属性GE 给属性初始化
	void InitializePrimaryAttributes() const;
```

&emsp;

+ `源文件`中：
```cpp
void AAuraCharacterBase::InitializePrimaryAttributes() const
{
	//这里是为了搞一个GE
	const FGameplayEffectContextHandle EffectContextHandle= GetAbilitySystemComponent()->MakeEffectContext();
	const FGameplayEffectSpecHandle EffectSpecHandle = GetAbilitySystemComponent()->MakeOutgoingSpec(GameplayEffectClass,Level,EffectContextHandle);
	//使用ASC组件调用应用GE
	GetAbilitySystemComponent()->ApplyGameplayEffectSpecToSelf(*EffectSpecHandle.Data.Get());
}
```

&emsp;

&emsp;

___________________________________________________________________________________________

###### 根据GE类,创建`FGameplayEffectSpecHandle`并应用到自身

```CPP
	//这里是为了搞一个GE
	FGameplayEffectContextHandle EffectContextHandle= GetAbilitySystemComponent()->MakeEffectContext();
	EffectContextHandle.AddSourceObject(this);
	const FGameplayEffectSpecHandle EffectSpecHandle = GetAbilitySystemComponent()->MakeOutgoingSpec(GameplayEffectClass,Level,EffectContextHandle);
	
	//使用ASC组件调用应用GE
	GetAbilitySystemComponent()->ApplyGameplayEffectSpecToSelf(*EffectSpecHandle.Data.Get());
```


![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/838486_222756.png?raw=true)
___________________________________________________________________________________________


##### `AAuraCharacter` 的 `InitAbilityActorInfo()` 函数中调用

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/844463_327081.png?raw=true)
___________________________________________________________________________________________


##### 创建文件夹

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/59883_457668.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/965655_918822.png?raw=true)
___________________________________________________________________________________________


##### `AbilitySystem \ GameplayEffects \ PrimaryAttributes`文件夹下创建初始化用的GE文件

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/376098_448663.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/548009_717922.png?raw=true)
___________________________________________________________________________________________


##### 别忘了给*BP_Aura* 配置`DefaultPrimaryAttributes`(使用初始化用的GE   *GE_AuraPrimaryAttributes*)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/597630_30182.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/619764_152779.png?raw=true)
___________________________________________________________________________________________


### 帮助理解的小案例

##### 创建一个Actor 拥有组件`BoxCollision` `BeginOverlap`时触发GE 根据角色属性触发_HP的逻辑

###### 新建文件夹/Actor/GE

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/503613_338575.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/242735_271610.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/371479_680532.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/291537_845177.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/569259_151180.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/703089_728654.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/437999_968644.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/481770_517036.png?raw=true)
___________________________________________________________________________________________


###### 设置GE

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/50918_528219.png?raw=true)
___________________________________________________________________________________________


##### 结果

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/499678_122060.png?raw=true)
___________________________________________________________________________________________


##### 属性 
![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/906204_173771.png?raw=true)
___________________________________________________________________________________________


### GE中的`Modifiers`（简单属性计算）
___________________________________________________________________________________________


##### 如果有三个`Modifier`,分别根据人物`活力``力量``坚韧`触发加血的GE逻辑

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/283180_607956.png?raw=true)
___________________________________________________________________________________________


##### 严格按照下标的顺序进行 逻辑运算

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/206479_41321.png?raw=true)
___________________________________________________________________________________________


### GE 中的 `Modifiers` 中的 `Coefficient`

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/950364_432461.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/669990_723459.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/385613_191279.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/72924_160997.png?raw=true)

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_014/640562_116628.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#Go主菜单)
___________________________________________________________________________________________
