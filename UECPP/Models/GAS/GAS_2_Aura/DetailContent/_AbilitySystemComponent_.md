___________________________________________________________________________________________
###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________
# AbilitySystemComponent

------

# 目录



------



## 介绍


<details>
<summary>AbilitySystemComponent 的基本介绍</summary>

>### AbilitySystemComponent 的基本概念
>
>`AbilitySystemComponent`（ASC）是Unreal Engine中的Gameplay Ability System（GAS）的核心组件之一。它用于管理和处理与游戏玩法相关的能力（Abilities）、效果（Effects）、属性（Attributes）以及状态（Gameplay Tags）等。ASC为角色或其他具有能力的对象（例如AI、可破坏的物体等）提供了一套框架，使得能力和效果的实现更加模块化和数据驱动。以下是ASC的一些主要功能和特点：
>
>### 1. **管理能力（Abilities）**
>
>- ASC负责激活、取消和管理与其关联的所有Gameplay Abilities。
>- 每个Ability都可以通过ASC来请求激活或取消，并且ASC会处理Ability的冷却、成本、条件等逻辑。
> 
> ### 2. **处理效果（Gameplay Effects）**
>
>- Gameplay Effects用于修改对象的属性值（例如生命值、速度等），并且ASC负责应用、移除和管理这些效果。
>- ASC可以处理效果的堆叠规则、持续时间和周期性效果（例如每秒伤害）。
> 
> ### 3. **属性系统（Attributes）**
>
>- ASC与Attribute Set配合使用，用于管理角色的各类属性，例如力量、敏捷、耐力等。
>- ASC提供了获取和修改属性值的接口，并可以通过Gameplay Effects来调整这些属性。
> 
> ### 4. **状态管理（Gameplay Tags）**
>
>- ASC利用Gameplay Tags来标识和管理角色或对象的状态，如“中毒”、“隐形”、“晕眩”等。
>- 这些标签可以与Abilities和Effects联动，用于控制能力的激活条件或效果的应用规则。
> 
> ### 5. **网络同步**
>
>- ASC设计上支持网络同步，使得在多人游戏中能力和效果的应用能够正确同步到客户端和服务器。
>- 它处理客户端预测、服务端验证等关键网络游戏开发中的同步问题。
> 
> ### 6. **事件与通知**
>
>- ASC提供了事件和委托，允许在Ability激活、效果应用、属性变化等事件发生时触发自定义逻辑。
>- 开发者可以利用这些事件来实现复杂的游戏机制，例如连击、特效触发等。
> 
> ### 7. **性能优化**
>
>- ASC和GAS框架本身是为性能优化而设计的，通过数据驱动的方式减少了蓝图逻辑的复杂性，并提升了大规模多人环境下的表现。
>
> ASC是GAS体系中非常灵活且功能强大的组件，适合用于实现复杂的游戏机制和效果。你在开发中可以通过继承和扩展它来实现自定义的行为，以满足特定的游戏需求。

------

</details>

------

>## 常用API

------

### 获取 `AbilitySystemComponent` 所属的 `Actor`

> ```CPP
> AbilitySystemComponent->GetAvatarActor();
> ```

------

### 为组件授予一个能力 `Ability`

> ```CPP
> GiveAbility(FGameplayAbilitySpec)
> ```

------

### 尝试激活指定的能力

> ```CPP
> TryActivateAbility(FGameplayAbilitySpecHandle)
> ```

------

### 取消指定的能力。用来中止正在执行的Ability

> ```CPP
> CancelAbility(FGameplayAbilitySpecHandle)
> ```

------

### 清除组件的所有能力

> ```CPP
> ClearAllAbilities()
> ```

------

### 获取当前可以激活的所有能力列表

> ```CPP
> GetActivatableAbilities()
> ```

------


















___________________________________________________________________________________________

[返回最上面](#Go主菜单)

___________________________________________________________________________________________
