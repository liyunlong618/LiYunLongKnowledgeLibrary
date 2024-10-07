___________________________________________________________________________________________
###### [GoLibraryMainMenu](../_LibraryMainMenu_.md)
___________________________________________________________________________________________
# UE小知识点
___________________________________________________________________________________________


## 目录

- [UE小知识点](#ue小知识点)
  - [目录](#目录)
    - [`GitHub` 拉取虚幻引擎源码](#github-拉取虚幻引擎源码)
    - [代码优化](#代码优化)
    - [检查目标对象是否实现了接口,使用 `Implements` 函数](#检查目标对象是否实现了接口使用-implements-函数)
    - [接口的全局静态函数](#接口的全局静态函数)
    - [使用 `懒加载单例模式`（Lazy Initialization Singleton Pattern）的两种方法](#使用-懒加载单例模式lazy-initialization-singleton-pattern的两种方法)



___________________________________________________________________________________________

### `GitHub` 拉取虚幻引擎源码

[拉虚幻引擎源码链接参考](https://www.bilibili.com/video/BV1ACt9eHE7J/?spm_id_from=333.999.0.0&vd_source=9e1e64122d802b4f7ab37bd325a89e6c)

[（1）下载和编译Unreal5源码 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/543310246)

------

### 代码优化

- 如果断点断不到想要的函数里面可能是开启了代码优化，下面是关闭代码优化的代码

  ```
  OptimizeCode = CodeOptimization.Never;
  ```

需要设置在项目的build.cs文件里面，如果是插件中的代码断不到，需要写在插件的build.cs文件里面

<details>
<summary>示例</summary>

> ```c#
> // Copyright Epic Games, Inc. All Rights Reserved.
> 
> using UnrealBuildTool;
> 
> public class Aura : ModuleRules
> {
>     public Aura(ReadOnlyTargetRules Target) : base(Target)
>     {
>        PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;
>        OptimizeCode = CodeOptimization.Never;/*关闭代码优化,防止断点断不到*/
>        PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore"});
>        //增强输入模块
>        PrivateDependencyModuleNames.AddRange(new string[] { "EnhancedInput" });
>        //GAS模块
>        PrivateDependencyModuleNames.AddRange(new string[] { "GameplayTags", "GameplayTasks", "GameplayAbilities" });
>        //NaviMesh导航模块
>        PrivateDependencyModuleNames.AddRange(new string[] { "NavigationSystem" });
>        //Niagara粒子模块
>        PrivateDependencyModuleNames.AddRange(new string[] { "Niagara" });
>        // Uncomment if you are using Slate UI
>         PrivateDependencyModuleNames.AddRange(new string[] { "Slate", "SlateCore" });
>        
>        // Uncomment if you are using online features
>        // PrivateDependencyModuleNames.Add("OnlineSubsystem");
> 
>        // To include OnlineSubsystemSteam, add it to the plugins section in your uproject file with the Enabled attribute set to true
>     }
> }
> ```

</details>

------

### 检查目标对象是否实现了接口,使用 `Implements` 函数

> ```CPP
> const bool 布尔变量 = 对象Actor->Implements<U开头的接口名>();
> ```
>
> **举例：**`bool ImplementsCombatInfenface = Actor()->Implements<UCombatInterface>();`

------

### 接口的全局静态函数

> ```CPP
> bool 布尔变量 = I开头的接口名::Execute_函数名(对象Actor);
> ```
>
> **举例：**`bool A = ICombatInterface::Execute_IsDead(Overlap.GetActor());`

------

### 使用 `懒加载单例模式`（Lazy Initialization Singleton Pattern）的两种方法

比如在A中申请结构体，在A源文件中，声明和定义一个结构体。在别的类中需要使用时，引用这个A的头文件即可

比如：

在A.cpp中

- 这里有两种方式

  - 一种是 `类内` 定义静态获取函数

    > ```CPP
    > struct AAA
    > {
    >  AAA()
    >  {
    >  }
    >  bool b = false;
    >  static const AAA& Get_AAA()/*创建一个外部获取的静态函数*/
    > 	{
    >  		static AAA a;/*该结构体的静态变量并返回*/
    > 	 	return a;
    > 	}
    > };
    > ```
    >
    > 调用时使用API：`AAA::Get_AAA().b`  即可拿到参数
    >
  
  - 另一种是 `类外` 定义静态获取函数
  
    > ```CPP
    > struct AAA
    > {
    >     AAA()
    >     {
    >     }
    >     bool b = false;
    > };
    > static const AAA& Get_AAA()/*创建一个外部获取的静态函数*/
    > {
    >     static AAA a;/*该结构体的静态变量并返回*/
    >     return a;
    > }
    > 
    > ```
    >
    > 调用时使用API：`Get_AAA().b`  即可拿到参数

------







# 待整理：

在 `Printf` 中使用 `%.1f` ，可以保留float小数点右边一位小数

![image-20240923234213745](./Image/UE_Tips/image-20240923234213745-1727106141136-1.png)

### 拿CSV表格数据

1. #### **创建CSV结构体**

   ```CPP
   USTRUCT(BlueprintType)
   struct FCSVCSV : public FTableRowBase
   {
       GENERATED_BODY()
   
       UPROPERTY(EditDefaultsOnly)
       float float1 = 0.f;
   
       UPROPERTY(EditDefaultsOnly)
       int32 num1 = 0.f;
   
       UPROPERTY(EditDefaultsOnly)
       FString name = FString();
   };
   ```

2. #### **蓝图继承该结构体，创建表格**

3. #### **保存表格数据（蓝图中配置）**

   ```CPP
   public:
       
       UPROPERTY(EditDefaultsOnly,BlueprintReadOnly)
       TObjectPtr<UDataTable> Infos;
   ```

4. #### **保存表格数据**

   ```CPP
   for (const FName& Name : Info->GetRowNames())
   {
   	const FCSVCSV* Csvcsv = Info->FindRow<FCSVCSV>(Name,FString());
   }
   ```

   

##### 临时对象的Outer可以使用UObject底层的API获取瞬态包

> ```CPP
> GetTransientPackage();
> ```
>
> 通常用于开发时需要短暂存储数据，且不希望这些数据被长期保存的场合。
>
> 下面是源码截图
>
> ![image-20241007231810443](./Image/UE_Tips/image-20241007231810443-1728314498877-2.png)
>
> ![image-20241007232003755](./Image/UE_Tips/image-20241007232003755-1728314498877-1.png)
