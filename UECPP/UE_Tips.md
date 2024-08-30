___________________________________________________________________________________________
###### [GoLibraryMainMenu](../_LibraryMainMenu_.md)
___________________________________________________________________________________________
# UE小知识点
___________________________________________________________________________________________


## 目录

[TOC]

___________________________________________________________________________________________

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

### 检查目标对象是否实现了接口,使用 `Implements` 函数

```CPP
const bool 布尔变量 = 对象Actor->Implements<U开头的接口名>();
```

**举例：**`bool ImplementsCombatInfenface = Actor()->Implements<UCombatInterface>();`

### 接口的全局静态函数

```CPP
bool 布尔变量 = I开头的接口名::Execute_函数名(对象Actor);
```

**举例：**`bool A = ICombatInterface::Execute_IsDead(Overlap.GetActor());`
