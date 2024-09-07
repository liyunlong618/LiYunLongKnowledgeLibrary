___________________________________________________________________________________________
###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________
# GameplayTag

------

# 目录

- [GameplayTag](#gameplaytag)
- [目录](#目录)
  - [介绍](#介绍)
    - [检查一个标签是否与另一个标签匹配，或者是否是该标签的子标签。使用 ：`MatchesTag`](#检查一个标签是否与另一个标签匹配或者是否是该标签的子标签使用-matchestag)
    - [`MatchesTagExact` 检查一个标签是否与另一个标签精确匹配，或者是否是该标签的子标签。](#matchestagexact-检查一个标签是否与另一个标签精确匹配或者是否是该标签的子标签)
    - [`MatchesAnyTags`检查一个标签是否与一组标签中的任意一个匹配。](#matchesanytags检查一个标签是否与一组标签中的任意一个匹配)
    - [`GetTagName` 获取 `GameplayTag` 的名称](#gettagname-获取-gameplaytag-的名称)
    - [`RequestGameplayTag` 创建一个 `GameplayTag`](#requestgameplaytag-创建一个-gameplaytag)
    - [使用 `UGameplayTagsManager` 创建一个 `GameplayTag`](#使用-ugameplaytagsmanager-创建一个-gameplaytag)
    - [监听 `GameplayTag` 变化](#监听-gameplaytag-变化)
  - [接下来，有一个注意点，虽然我们 `监听Tag变化的回调` 可以帮助我们知道何时开始技能冷却，但是，可能并没有那么准确，会有滞后性，但是 `GE的添加`回调 不会有滞后，所以为了监听的准确，在 `技能开始时` 需要 `监听GE` 的添加，`结束时` ，`监听Tag新计数`即可](#接下来有一个注意点虽然我们-监听tag变化的回调-可以帮助我们知道何时开始技能冷却但是可能并没有那么准确会有滞后性但是-ge的添加回调-不会有滞后所以为了监听的准确在-技能开始时-需要-监听ge-的添加结束时-监听tag新计数即可)



------



## 介绍


<details>
<summary>GameplayTag 的基本介绍</summary>

> `GameplayTag` 是虚幻引擎中的一个系统，用于为游戏中的对象、属性、事件等添加标识标签。这些标签是通过字符串形式定义的，并且通常以分层的方式组织。`GameplayTag` 系统提供了一种灵活而强大的方式来管理游戏逻辑，特别是在复杂的角色扮演游戏、多人在线游戏以及其他需要处理大量状态和条件的游戏中。
>
> ### 1. **GameplayTag 的基本概念**
>
> - **标签（Tag）**: `GameplayTag` 是一个表示特定状态、属性或行为的标识符。例如，一个角色可能具有`"Character.Status.Stunned"`（角色处于眩晕状态）这样的标签。
> - **层次结构**: `GameplayTag` 是层次化的，标签之间可以存在父子关系。例如，`"Character.Status.Stunned"` 可以是 `"Character.Status"` 的子标签，这意味着它继承了父标签的所有特性。
> - **标签容器（Tag Container）**: `GameplayTagContainer` 是一个存储多个 `GameplayTag` 的容器，用于管理对象的多种状态或属性。你可以通过这个容器来检查对象是否具有特定的标签或组合标签。
>
> ### 2. **GameplayTag 的优势**
>
> - **灵活性**: `GameplayTag` 系统允许开发者以松散耦合的方式管理状态和逻辑。不同的模块或系统可以通过标签进行通信，而不需要直接依赖于彼此的具体实现。
> - **可扩展性**: `GameplayTag` 系统可以轻松扩展，只需添加新标签即可管理新的状态或行为，无需修改已有的代码结构。
> - **层次结构管理**: 通过标签的层次结构，开发者可以通过高层标签对所有相关子标签进行操作，这使得状态管理更加简单和直观。
>
> ### 3. **GameplayTag 的使用场景**
>
> - **状态管理**: 角色或对象的状态可以通过标签来管理。例如，一个角色可以有 `"Character.Status.Poisoned"`、`"Character.Status.Stunned"` 这样的标签来表示当前状态。游戏逻辑可以通过检查这些标签来决定角色是否能够进行某些动作。
> - **技能和效果**: 游戏中的技能和效果可以使用 `GameplayTag` 来定义和检测。例如，技能可以添加 `"Skill.Fire"` 或 `"Skill.AOE"` 标签，而角色可以检测自己是否易受 `"Skill.Fire"` 类技能的影响。
> - **权限和规则**: 在多人游戏中，`GameplayTag` 可以用于定义权限和规则。例如，某个区域可能有 `"Area.Restricted"` 标签，只有具有特定权限标签的玩家才能进入。
>
> ------

</details>

------

>## GameplayTag 对比 API：

------

### 检查一个标签是否与另一个标签匹配，或者是否是该标签的子标签。使用 ：`MatchesTag`

> ```cpp
>bool bIsMatch = SomeTag.MatchesTag(OtherTag);
> ```
>
> - 举例:
> 
>   > ```cpp
>  > FGameplayTag SomeTag = FGameplayTag::RequestGameplayTag(FName("Character.Status.Stunned"));
>   > FGameplayTag OtherTag = FGameplayTag::RequestGameplayTag(FName("Character.Status"));
>  > 
>   > bool bIsMatch = SomeTag.MatchesTag(OtherTag);
>   > // 返回 true，因为 "Character.Status.Stunned" 是 "Character.Status" 的子标签。
>   > ```

------

### `MatchesTagExact` 检查一个标签是否与另一个标签精确匹配，或者是否是该标签的子标签。

> #### **需要注意这里是源码中的备注： `"A.1".MatchesTagExact("A") will return False`**
>
> #### 也就是说只能父查子节点，子查父用这个会返回 false！！！！！！！！！！！！！！！！！！
>
> ```cpp
> bool bIsMatch = SomeTag.MatchesTagExact(OtherTag);
> ```
>
> - 举例:
>
>   > ```cpp
>   > FGameplayTag SomeTag = FGameplayTag::RequestGameplayTag(FName("Character.Status.Stunned"));
>   > FGameplayTag OtherTag = FGameplayTag::RequestGameplayTag(FName("Character.Status"));
>   > 
>   > bool bIsMatch1 = SomeTag.MatchesTagExact(OtherTag);
>   > // 返回 false，因为 "Character.Status.Stunned" 是 "Character.Status" 的子标签。
>   > 
>   > bool bIsMatch2 = OtherTag.MatchesTagExact(SomeTag);
>   > // 返回 true，因为 "Character.Status.Stunned" 是 "Character.Status" 的子标签。
>   > ```

------

### `MatchesAnyTags`检查一个标签是否与一组标签中的任意一个匹配。

> ```c++
> bool bIsMatch = SomeTag.MatchesAnyTags(TagContainer);
> ```
>
> - 举例：
>
>   ```cpp
>   FGameplayTagContainer TagContainer;
>   TagContainer.AddTag(FGameplayTag::RequestGameplayTag(FName("Character.Status")));
>   TagContainer.AddTag(FGameplayTag::RequestGameplayTag(FName("Character.Action.Jump")));
>                           
>   FGameplayTag SomeTag = FGameplayTag::RequestGameplayTag(FName("Character.Status.Stunned"));
>                           
>   bool bIsMatch = SomeTag.MatchesAnyTags(TagContainer);
>   // 返回 true，因为 "Character.Status.Stunned" 是 "Character.Status" 的子标签。
>   ```

------

### `GetTagName` 获取 `GameplayTag` 的名称

> ```cpp
> FName TagName = MyTag.GetTagName();
> ```

------

### `RequestGameplayTag` 创建一个 `GameplayTag` 

> ```c++
> FGameplayTag MyTag = FGameplayTag::RequestGameplayTag(FName("Character.Status.Stunned"));
> ```

------

### 使用 `UGameplayTagsManager` 创建一个 `GameplayTag` 

> ```CPP
> UGameplayTagsManager::Get().AddNativeGameplayTag(FName("CombatSocket.LeftHand"), FString("CombatSocket LeftHand"));
> ```
>
> #### 这样就创建了一个 `CombatSocket` 下的 `LeftHand` 标签，备注是 `CombatSocket LeftHand`

------

### 监听 `GameplayTag` 变化

> ```CPP
> AbilitySystemComponent->RegisterGameplayTagEvent(/*要监听的Tag*/,EGameplayTagEventType::NewOrRemoved/*监听类型一般是这个*/).AddUObject(this,&AAuraEnemy::HitReactTagChanged)/*后面这里是绑定的回调*/;
> ```
>
> ##### **回调函数需要的参数为：**
>
> ```cpp
> void AAuraEnemy::HitReactTagChanged(const FGameplayTag CallbackTag/*要监听的Tag*/, int32 NewCount/*当前Tag新的标签计数*/)
> ```
>
> **使用案例参考：**[GAS 057 敌人受击反应](./GAS_057.md)

------

## 接下来，有一个注意点，虽然我们 `监听Tag变化的回调` 可以帮助我们知道何时开始技能冷却，但是，可能并没有那么准确，会有滞后性，但是 `GE的添加`回调 不会有滞后，所以为了监听的准确，在 `技能开始时` 需要 `监听GE` 的添加，`结束时` ，`监听Tag新计数`即可

> 因为 `OnActiveGameplayEffectAddedDelegateToSelf` 直接监听到 `Gameplay Effect (GE)` 的 `添加事件` ，比通过标签变化回调的触发更及时和直接。
>
> 为什么需要绑定 `OnActiveGameplayEffectAddedDelegateToSelf`
>
> - ### **GE 添加的及时性**:
>
>   - 通过 `OnActiveGameplayEffectAddedDelegateToSelf`，你可以立即知道冷却 GE 何时被应用到 `AbilitySystemComponent` 上。这是最直接的方式来捕捉冷却开始的事件。
>
> - ### **冷却标签的延迟**:
>
>   - 虽然冷却 GE 会在应用时添加冷却标签，但标签的变化事件有时会稍有延迟，或者在标签的变化逻辑上受到其他条件的影响。
>
>   - 通过监听 GE 的添加，可以确保回调在冷却开始时立即响应，而不仅仅依赖于标签的增加。
>
> #### **查看 `ASC源码` 中对 `OnActiveGameplayEffectAddedDelegateToSelf`的备注为：`每当添加基于持续时间的 GE 时都会调用客户端和服务器`**

------



















#### **`HasAnyExact` 和 `HasAllExact`**
`"A.1".MatchesTagExact("A") will return False`




- **功能**: 直接比较标签，不考虑继承关系。

- 用法:

  ```cpp
  bool bHasAnyExact = TagContainer.HasAnyExact(SomeTag);
  bool bHasAllExact = TagContainer.HasAllExact(SomeTag);
  ```
  
- 例子

  :

  ```cpp
  FGameplayTagContainer TagContainer;
  TagContainer.AddTag(FGameplayTag::RequestGameplayTag(FName("Character.Status.Stunned")));
  
  FGameplayTag SomeTag = FGameplayTag::RequestGameplayTag(FName("Character.Status"));
  
  bool bHasAnyExact = TagContainer.HasAnyExact(SomeTag);
  // 返回 false，因为 "Character.Status.Stunned" 不是 "Character.Status" 的精确匹配。
  ```


#### **2.3 `GetParentTag`**

- **功能**: 获取父标签（如果有）

- 用法:

  ```cpp
  FGameplayTag ParentTag = MyTag.GetParentTag();
  ```

### 3. **实际使用案例**

假设你有一个游戏角色，当它进入“中毒”状态时，你可能希望检查该角色是否处于任何负面状态（如“眩晕”或“中毒”）。你可以这样实现：

```cpp
FGameplayTagContainer NegativeStatusTags;
NegativeStatusTags.AddTag(FGameplayTag::RequestGameplayTag(FName("Character.Status.Stunned")));
NegativeStatusTags.AddTag(FGameplayTag::RequestGameplayTag(FName("Character.Status.Poisoned")));

FGameplayTag CurrentStatus = FGameplayTag::RequestGameplayTag(FName("Character.Status.Poisoned"));

if (CurrentStatus.MatchesAnyTags(NegativeStatusTags))
{
    UE_LOG(LogTemp, Warning, TEXT("The character is in a negative status."));
}
```

这种方式能够方便地通过`GameplayTag`系统管理游戏中的各种状态和条件。如果你有更具体的需求或场景，我可以帮助你进一步优化。


___________________________________________________________________________________________

[返回最上面](#Go主菜单)

___________________________________________________________________________________________