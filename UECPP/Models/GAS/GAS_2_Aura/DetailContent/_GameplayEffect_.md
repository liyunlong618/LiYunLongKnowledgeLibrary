___________________________________________________________________________________________
###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________
# GameplayEffect

------

# 目录

- [GameplayEffect](#gameplayeffect)
- [目录](#目录)
  - [介绍](#介绍)
  - [Modifiers](#modifiers)
    - [ModifierMagnitude](#modifiermagnitude)
      - [MagnitudeCalculationType](#magnitudecalculationtype)


------



## 介绍


<details>
<summary>GameplayEffect 的基本介绍</summary>

> ### GameplayEffect 的基本概念
>
> `GameplayEffect` 是一种数据驱动的对象，包含了影响游戏属性的各种信息。它可以通过多种方式影响游戏角色或对象的属性值，包括持续时间、堆叠、条件和修改器等。
>
> ### GameplayEffect 的关键属性
>
> 1. **Modifiers（修改器）**:
>    - **描述**：定义了具体的属性修改规则，如增加或减少属性值。每个 Modifier 都包含属性类型、修改操作（如加法、乘法）和修改量。
>    - **示例**：一个增加角色生命值的 Modifier 可以设置为对“生命值”属性进行加法操作，增加 50 点。
> 2. **Duration（持续时间）**:
>    - **描述**：决定了效果持续的时间长度，可以是瞬时的（Instant）、持续一段时间的（Duration）、或者永久的（Infinite）。
>    - **示例**：一个持续 10 秒的护盾效果，或者一个永久增加攻击力的效果。
> 3. **Period（周期性）**:
>    - **描述**：如果设置了周期，`GameplayEffect` 将在指定的时间间隔内重复应用。这个属性通常与持续时间一起使用。
>    - **示例**：每 5 秒恢复 10 点生命值，持续 30 秒。
> 4. **Stacking（堆叠规则）**:
>    - **描述**：定义了效果如何堆叠，包括堆叠上限和堆叠规则（如独立堆叠、替换、合并等）。
>    - **示例**：一个可以堆叠 3 层的攻击力提升效果，每层增加 10 点攻击力。
> 5. **Gameplay Tags**:
>    - **描述**：用于标记效果的类型、目标、来源等信息，可以用于筛选、组合和管理效果。
>    - **示例**：标记为“火焰伤害”的效果，便于在游戏逻辑中进行处理。
> 6. **Application Requirements（应用条件）**:
>    - **描述**：定义了效果应用于目标的条件，通常基于目标属性、状态、标签等。
>    - **示例**：只能对生命值低于 50% 的角色应用的治疗效果。
>
> ### GameplayEffect 的类型
>
> 1. **Instant（瞬时效果）**:
>    - 立即生效并影响目标属性，没有持续时间。例如，立即恢复 100 点生命值。
> 2. **Duration（持续性效果）**:
>    - 在一段时间内持续影响目标属性，可以是周期性的。例如，降低敌人移动速度 30%，持续 10 秒。
> 3. **Infinite（永久性效果）**:
>    - 一旦应用，效果将一直存在，直到被移除。例如，永久增加角色的攻击力。
>
> ------

</details>







## `Modifiers`
>- **Modifier（修改器）** 是一种机制，用于改变游戏中角色或对象的属性值。

### `ModifierMagnitude`
>- **Modifier Magnitude** 是一个关键概念，用于控制 Gameplay Effect 对属性（Attributes）施加的影响程度。

#### `MagnitudeCalculationType`
>- **MagnitudeCalculationType** 决定了 `GameplayEffectModifier` 的数值大小是如何计算的。
>- #### **分为以下几种类型：**
>  
>  1. **ScalableFloat** (`EGameplayEffectMagnitudeCalculation::ScalableFloat`)
>    - 可以通过曲线表获取值。
>    - 直接设置固定值。
>  2. **AttributeBased** (`EGameplayEffectMagnitudeCalculation::AttributeBased`)
>    - 基于另一个属性的当前值来计算修改器的数值。
>  3. **CustomCalculationClass** (`EGameplayEffectMagnitudeCalculation::CustomCalculationClass`)
>    - 使用自定义的 C++ 或 Blueprint 脚本来计算修改器的数值。
>  4. **SetByCaller** (`EGameplayEffectMagnitudeCalculation::SetByCaller`)
>    - 数值由调用方（如技能或效果）在运行时动态设置，比如GA中的值。调用方需要在应用效果前设置好数值。













------

> ## 常用API：

------

### 将一个 `Gameplay Effect` 应用到自身

> ```CPP
> ApplyGameplayEffectToSelf(UGameplayEffect*, float, FGameplayEffectContextHandle)
> ```

------

### 将一个 `Gameplay Effect` 应用到指定的目标

> ```CPP
> ApplyGameplayEffectToTarget(UGameplayEffect*, UAbilitySystemComponent*, float, FGameplayEffectContextHandle)
> ```

------

### 移除指定的活动 `Gameplay Effect` 通常用于取消持续性效果。

> ```CPP
> RemoveActiveGameplayEffect(FActiveGameplayEffectHandle)
> ```

------

### 获取当前所有激活的 `Gameplay Effects`列表。用于调试或查询角色当前状态。

> ```CPP
> GetActiveEffects()
> ```

------



































___________________________________________________________________________________________

[返回最上面](#Go主菜单)

___________________________________________________________________________________________