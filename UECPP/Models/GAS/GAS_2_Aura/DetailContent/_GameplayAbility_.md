___________________________________________________________________________________________
###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________
# GameplayAbility

------

# 目录



------



## 介绍


<details>
<summary>GameplayEffect 的基本介绍</summary>

>### Gameplay Ability 的基本概念
>
>`GameplayAbility` 是一种数据驱动的对象，可以通过 Blueprint 或 C++ 实现。它封装了技能的启动、执行、冷却以及结束的完整流程，并且能够与 `GameplayEffect`、`GameplayTags`、`GameplayCue` 等其他 GAS 组件紧密集成。
>
>### Gameplay Ability 的关键组件
>
>1. **Ability Input**:
>
>   - **描述**：指定触发该技能的输入事件或按键，可以通过输入映射（Input Mapping）配置。
>   - **示例**：按下键盘上的“F”键触发一个火球技能。
>
>2. **Ability Activation**:
>
>   - **描述**：定义了技能何时以及如何被激活。可以在满足特定条件时手动或自动激活。
>   - **示例**：当玩家按下技能按钮并且法力值足够时，激活该技能。
>
>3. **Ability Cost**:
>
>   - **描述**：技能激活时的消耗，例如法力值、体力值等，可以通过 `GameplayEffect` 来实现。
>   - **示例**：每次使用火球技能消耗 20 点法力值。
>
>4. **Cooldown**:
>
>   - **描述**：定义技能的冷却时间，即再次激活技能之前需要等待的时间。
>   - **示例**：火球技能使用后需要等待 5 秒才能再次使用。
>
>5. **Ability Tasks**:
>
>   - **描述**：用于定义技能的具体执行流程，可以通过内置的 Ability Task 或自定义的任务来实现复杂的行为。
>   - **示例**：创建一个任务链，依次执行移动、施法、击中效果等操作。
>
>6. **Gameplay Tags**:
>
>   - **描述**：用于标记技能的特性、类型或其他属性，可以用于筛选、限制或触发其他行为。
>   - **示例**：给火球技能添加“火焰”标签，可以在游戏中识别并处理与火焰相关的逻辑。
>
>7. **Commit Ability**:
>
>   - **描述**：在技能成功激活后，执行与资源消耗、状态改变等相关的操作。
>
>   - **示例**：成功释放火球技能后，扣除玩家的法力值并进入冷却状态。

------

</details>



------

> ## 常用API：

------

### 启动Ability的主要逻辑。通常在子类中重写这个函数，定义Ability的具体行为。

> ```cpp
> ActivateAbility()
> ```

------

### 检查能力是否可以被激活。通常用于检测条件是否满足，如资源充足、没有被沉默等。

> ```cpp
> CanActivateAbility(FGameplayAbilitySpecHandle, const FGameplayAbilityActorInfo*, const FGameplayTagContainer*)
> ```

------

### 结束当前激活的能力。可以在能力执行完毕或被中断时调用，确保清理和资源释放。

> ```cpp
> EndAbility(FGameplayAbilitySpecHandle, const FGameplayAbilityActorInfo*, const FGameplayAbilityActivationInfo, bool)
> ```

------

### 取消当前激活的能力。可以用在需要中止能力的情况下，比如玩家被打断或主动取消。

> ```cpp
> CancelAbility()
> ```

------

### 应用能力的冷却时间。通常在激活能力时调用，使得能力在冷却期内无法再次激活。

> ```cpp
> ApplyCooldown(FGameplayAbilitySpecHandle, const FGameplayAbilityActorInfo*, FGameplayAbilityActivationInfo)
> ```

------

### 检查能力的成本是否足够（如法力值、体力等）。在激活前调用以确保能力能够被执行。

> ```cpp
> CheckCost(FGameplayAbilitySpecHandle, const FGameplayAbilityActorInfo*)
> ```

------

### 应用能力的成本。通常在能力成功激活时调用，消耗对应的资源。

> ```cpp
> ApplyCost(FGameplayAbilitySpecHandle, const FGameplayAbilityActorInfo*, FGameplayAbilityActivationInfo)
> ```

------

### 创建一个Gameplay Effect Spec，用于定义Effect的属性和应用规则。可以通过它来调整目标属性或状态。

> ```cpp
> GetGameplayEffectSpec(FGameplayEffect*, const FGameplayAbilitySpecHandle)
> ```

------

### 将指定的Gameplay Effect应用到目标上。用于在Ability激活时对目标施加效果，如伤害或治疗。

> ```cpp
> ApplyGameplayEffectSpecToTarget(FGameplayEffectSpec*, UAbilitySystemComponent*)
> ```

------

### 创建一个目标数据结构，用于定义能力的作用对象。可以是单个Actor，也可以是多个目标。

> ```cpp
> MakeTargetDataFromActor(AActor*)
> ```

------

### 当能力被授予时触发的回调。可用于初始化或其他逻辑处理。

> ```cpp
> OnGiveAbility(FGameplayAbilityActorInfo*, FGameplayAbilitySpec*)
> ```

------

### 当能力被移除时触发的回调。用于清理资源或重置状态。

> ```cpp
> OnRemoveAbility(FGameplayAbilityActorInfo*, FGameplayAbilitySpec*)
> ```

------

### 绑定能力到输入组件，使得能力可以通过输入（如按键）激活。用于处理玩家输入和能力触发的关联。

> ```cpp
> BindAbilityActivationToInputComponent(UInputComponent*, FGameplayAbilityInputBinds)
> ```

------

### 用于创建和执行能力任务（Ability Tasks），如计时、等待事件、移动等。Ability Tasks是实现复杂行为的重要工具。

> ```cpp
> UAbilityTask::CreateAbilityTask()
> ```

------

### 等待目标数据（Target Data）的任务，用于处理需要目标选择的能力（如锁定敌人、指定位置）。

> ```cpp
> UAbilityTask_WaitTargetData::WaitTargetData()
> ```

------

### 播放动画Montage并等待其结束。常用于执行带有动画效果的能力。

> ```cpp
> UAbilityTask_PlayMontageAndWait::PlayMontageAndWait()
> ```

------

### 获取Ability的输入ID，用于与输入绑定。帮助识别哪种输入触发了该Ability。

> ```cpp
> GetInputID()
> ```

------

### 当Ability对应的输入被按下时触发。用于响应玩家的输入行为。

> ```cpp
> InputPressed(FGameplayAbilitySpecHandle)
> ```

------

### 当Ability对应的输入被释放时触发。用于检测玩家的输入释放事件。

> ```cpp
> InputReleased(FGameplayAbilitySpecHandle)
> ```

------


























___________________________________________________________________________________________

[返回最上面](#Go主菜单)

___________________________________________________________________________________________
