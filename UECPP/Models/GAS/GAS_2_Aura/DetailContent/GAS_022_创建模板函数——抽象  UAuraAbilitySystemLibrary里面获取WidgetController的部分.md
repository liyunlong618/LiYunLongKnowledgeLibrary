___________________________________________________________________________________________

###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________

# GAS_022_创建模板函数——抽象  UAuraAbilitySystemLibrary里面获取WidgetController的部分
___________________________________________________________________________________________
## 处理关键点
1. 模板函数的使用
2. if constexpr 是一种条件编译语句,它允许在编译时进行条件检查,并且只有满足条件的分支代码会被编译。这与普通的 if 语句不同,普通的 if 语句是在运行时进行条件检查。示例:
```cpp
if constexpr (std::is_same_v<T, UOverlayWidgetController>)
{
    Ptr = HUD_>GetOverlayWidgetController(Params);
}
else if constexpr (std::is_same_v<T, UAttributeMenuWidgetController>)
{
    Ptr = HUD_>GetAttributeMenuWidgetController(Params);
}
```
___________________________________________________________________________________________


# 目录
- [GAS 022 创建模板函数——抽象  UAuraAbilitySystemLibrary 里面获取WidgetController的部分](#gas-022-创建模板函数抽象--uauraabilitysystemlibrary-里面获取widgetcontroller的部分)
	- [处理关键点](#处理关键点)
	- [目录](#目录)
		- [蓝图函数库`UAuraAbilitySystemLibrary`中,使用`if constexpr `语句在函数模板中`预编译时进行类型判断`](#蓝图函数库uauraabilitysystemlibrary中使用if-constexpr-语句在函数模板中预编译时进行类型判断)
			- [`UAuraAbilitySystemLibrary`中](#uauraabilitysystemlibrary中)
		- [错误示范](#错误示范)



___________________________________________________________________________________________



### 蓝图函数库`UAuraAbilitySystemLibrary`中,使用`if constexpr `语句在函数模板中`预编译时进行类型判断`
#### `UAuraAbilitySystemLibrary`中

- 头文件

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_022/719988_993402.png?raw=true)



```cpp
// Copyright belongs to Li Yunlong.

#pragma once

#include "CoreMinimal.h"
#include "AuraAbilitySystemComponent.h"
#include "AuraAttributeSet.h"
#include "Kismet/BlueprintFunctionLibrary.h"
#include "Kismet/GameplayStatics.h"
#include "PlayerState/AuraPlayerState.h"
#include "UI/HUD/AuraHUD.h"
#include "UI/WidgetController/UAuraWidgetController.h"
#include "AuraAbilitySystemLibrary.generated.h"

class UOverlayWidgetController;
/**
 * 
 */
UCLASS()
class AURA_API UAuraAbilitySystemLibrary : public UBlueprintFunctionLibrary
{
	GENERATED_BODY()

public:
	
		//创建工具函数可以在 蓝图中获取数据		BlueprintPure表示该函数可以在蓝图中被调用并且是一个纯函数。
		UFUNCTION(BlueprintPure,Category="AuraAbilitySystemLibrary|WidgetController",meta=(WorldContext="WorldContextObject"))
		static UOverlayWidgetController* GetOverlayWidgetController(const UObject* WorldContextObject);
		UFUNCTION(BlueprintPure,Category="AuraAbilitySystemLibrary|WidgetController",meta=(WorldContext="WorldContextObject"))
		static UAttributeMenuWidgetController* GetAttributeMenuWidgetController(const UObject* WorldContextObject);

		//抽象 Get WidgetController部分
		template<typename T>
		static T* GetWidgetController(const UObject* WorldContextObject);
};

//抽象 Get WidgetController部分
template <typename T>
T* UAuraAbilitySystemLibrary::GetWidgetController(const UObject* WorldContextObject)
{
	T* Ptr = nullptr;
	if (APlayerController* PlayerController = UGameplayStatics::GetPlayerController(WorldContextObject, 0))
	{
		if (AAuraHUD* HUD = Cast<AAuraHUD>(PlayerController->GetHUD()))
		{
			AAuraPlayerState* AuraPlayerState = PlayerController->GetPlayerState<AAuraPlayerState>();
			UAuraAbilitySystemComponent* AuraAbilitySystemComponent = Cast<UAuraAbilitySystemComponent>(AuraPlayerState->GetAbilitySystemComponent());
			UAuraAttributeSet* AuraAttributeSet = Cast<UAuraAttributeSet>(AuraPlayerState->GetAttributeSet());
			const FWidgetControllerParams Params = FWidgetControllerParams(PlayerController, AuraPlayerState, AuraAbilitySystemComponent, AuraAttributeSet);
			/*这部分代码使用了 C++17 引入的 if constexpr 语句和 std::is_same_v 类型特征来在编译时进行类型检查和选择性地编译代码分支。
			 * 
			 * if constexpr 语句:
			 * if constexpr 是一种条件编译语句，它允许在编译时进行条件检查，并且只有满足条件的分支代码会被编译。这与普通的 if 语句不同，普通的 if 语句是在运行时进行条件检查。
			 * 
			 * std::is_same_v<T, UOverlayWidgetController>:
			 * std::is_same_v 是 std::is_same 的简化形式，用于比较两个类型是否相同。
			 * std::is_same_v<T, UOverlayWidgetController> 在编译时会检查模板参数 T 是否等于 UOverlayWidgetController。如果相等，这个表达式的值为 true。
			 *
			 * 通过使用 if constexpr 和 std::is_same_v，你可以在编译时根据模板参数类型选择性地编译不同的代码分支。
			 * 这在编写模板代码时非常有用，因为它允许你在编译时做出决定，从而避免了在运行时进行不必要的类型检查和分支判断，提高了代码的性能和类型安全性。
			 * 
			 * 具体来说，在这个例子中:
			 * 如果 T 是 UOverlayWidgetController，编译器会编译 Ptr = HUD->GetOverlayWidgetController(Params);，并忽略 else 分支。
			 * 如果 T 是 UAttributeMenuWidgetController，编译器会编译 Ptr = HUD->GetAttributeMenuWidgetController(Params);，并忽略 if 分支。
			 * 这种方式确保了模板函数在不同的类型参数下具有正确的行为。
			 */
			if constexpr (std::is_same_v<T, UOverlayWidgetController>)
			{
				Ptr =  HUD->GetOverlayWidgetController(Params);
			}
			else if constexpr (std::is_same_v<T, UAttributeMenuWidgetController>)
			{
				Ptr =  HUD->GetAttributeMenuWidgetController(Params);
			}
		}
	}
	return Ptr;
}
```
___________________________________________________________________________________________


- 源文件

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_022/122441_18049.png?raw=true)

```cpp
//==================================================这里是旧的逻辑====================================================
//UOverlayWidgetController* UAuraAbilitySystemLibrary::GetOverlayWidgetController(const UObject* WorldContextObject)
//{
//	UOverlayWidgetController* TempOverlayWidgetController = nullptr;
//	if (APlayerController* PlayerController = UGameplayStatics::GetPlayerController(WorldContextObject, 0))
//	{
//		if (AAuraHUD* HUD = Cast<AAuraHUD>(PlayerController->GetHUD()))
//		{
//			AAuraPlayerState* AuraPlayerState = PlayerController->GetPlayerState<AAuraPlayerState>();
//			UAuraAbilitySystemComponent* AuraAbilitySystemComponent = Cast<UAuraAbilitySystemComponent>(AuraPlayerState->GetAbilitySystemComponent());
//			UAuraAttributeSet* AuraAttributeSet = Cast<UAuraAttributeSet>(AuraPlayerState->GetAttributeSet());
//			const FWidgetControllerParams Params = FWidgetControllerParams(PlayerController, AuraPlayerState, AuraAbilitySystemComponent, AuraAttributeSet);
//			TempOverlayWidgetController = HUD->GetOverlayWidgetController(Params);
//		}
//	}
//	return TempOverlayWidgetController;
//}

//UAttributeMenuWidgetController* UAuraAbilitySystemLibrary::GetAttributeMenuWidgetController(
//	const UObject* WorldContextObject)
//{
//	UAttributeMenuWidgetController* TempOverlayWidgetController = nullptr;
//	if (APlayerController* PlayerController = UGameplayStatics::GetPlayerController(WorldContextObject, 0))
//	{
//		if (AAuraHUD* HUD = Cast<AAuraHUD>(PlayerController->GetHUD()))
//		{
//			AAuraPlayerState* AuraPlayerState = PlayerController->GetPlayerState<AAuraPlayerState>();
//			UAuraAbilitySystemComponent* AuraAbilitySystemComponent = Cast<UAuraAbilitySystemComponent>(AuraPlayerState->GetAbilitySystemComponent());
//			UAuraAttributeSet* AuraAttributeSet = Cast<UAuraAttributeSet>(AuraPlayerState->GetAttributeSet());
//			const FWidgetControllerParams Params = FWidgetControllerParams(PlayerController, AuraPlayerState, AuraAbilitySystemComponent, AuraAttributeSet);
//			TempOverlayWidgetController = HUD->GetAttributeMenuWidgetController(Params);
//		}
//	}
//	return TempOverlayWidgetController;
//}
```

```CPP
UOverlayWidgetController* UAuraAbilitySystemLibrary::GetOverlayWidgetController(const UObject* WorldContextObject)
{
	return GetWidgetController<UOverlayWidgetController>(WorldContextObject);
}
UAttributeMenuWidgetController* UAuraAbilitySystemLibrary::GetAttributeMenuWidgetController(const UObject* WorldContextObject)
{
    return GetWidgetController<UAttributeMenuWidgetController>(WorldContextObject);
}
```

> ## 这里的抽象比较难，有时间可以看一看《C++模板》这本书

___________________________________________________________________________________________


### 错误示范

！！！:HUD AAuraHUD 中这么干,无法判断空指针,每次都会实例化



> ## 这里只是记录先不仔细研究




- 头文件

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_022/113702_587283.png?raw=true)
___________________________________________________________________________________________


 - 源文件

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_022/845243_221712.png?raw=true)

___________________________________________________________________________________________

[返回最上面](#Go主菜单)
___________________________________________________________________________________________