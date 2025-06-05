___________________________________________________________________________________________
###### [GoLibraryMainMenu](../_LibraryMainMenu_.md)
___________________________________________________________________________________________
# **创建自定义ini文件并在虚幻项目编辑中修改和打包**


___________________________________________________________________________________________


## 目录

[TOC]

___________________________________________________________________________________________

接下来根据在`模块/插件中使用` or 在项目中`直接使用`

## 插件中需要注册



------

## 项目直接使用

- **需要继承自`UDeveloperSettings`可以自动注册**

需要注意：

- **编辑器的方法最好使用 `WITH_EDITOR` 宏包裹 防止打包时报错 ！！！！！**

**eg:**

```cpp
// .h
UCLASS(Config=TileMatchingConfig, defaultconfig, meta = (DisplayName = "Tile Matching Setting"))
class FRUITPARADISE_API UTileMatchingConfig : public UDeveloperSettings
{
    GENERATED_BODY()
    
public:
    
    UTileMatchingConfig() = default;
    
    UPROPERTY(config, EditDefaultsOnly, Category = "Config | CreateOrders")
    TSoftClassPtr<UUserWidget> TileOrderClass;

    UPROPERTY(Config, EditDefaultsOnly, Blueprintable, Category = "TileMatching | Config")
    TSoftObjectPtr<UTileMatchingInfo> TileMatchingInfo;
    
#if WITH_EDITOR
    virtual void PostEditChangeProperty(FPropertyChangedEvent& PropertyChangedEvent);
#endif
};

// .cpp
// 编辑器的方法最好使用 WITH_EDITOR 宏包裹 防止打包时报错
#if WITH_EDITOR
void UTileMatchingConfig::PostEditChangeProperty(FPropertyChangedEvent& PropertyChangedEvent)
{
	Super::PostEditChangeProperty(PropertyChangedEvent);
	//if (PropertyChangedEvent.Property->GetName() != GET_MEMBER_NAME_CHECKED(UTileMatchingConfig, bEnableDebug))
	//{
	//	return;
	//}
	const FString Console = FString::Printf(TEXT("FPTM.EnableDebug %d"), bEnableDebug ? 1 : 0);
	UKismetSystemLibrary::ExecuteConsoleCommand(this, Console, nullptr);
	if (TileMatchingInfo != nullptr)
	{
		TileMatchingInfo->UpdateParams();
	}
}
#endif
```

UClass宏的标识

```cpp
//  将配置归属到 Project Settings（而非 Editor Settings）
Config=Game
// 将配置归属到 Engine 页签下
Config=TileMatchingConfig
// 自动在源码的 Config/DefaultGame.ini 中生成并保存你的默认值节
defaultconfig
// 决定 Project Settings 面板中显示的节标题
meta=(DisplayName="xxx")     
```

参考文档：

- [[UE4\] 自定义ini文件使用流程以及打包后修改 - 知乎](https://zhuanlan.zhihu.com/p/555236746)
- [UE4中自定义ini文件的打包发布及用法技巧 - 知乎](https://zhuanlan.zhihu.com/p/341911934)