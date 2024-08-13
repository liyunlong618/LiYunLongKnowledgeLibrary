**Mermaid**，它是一种用于生成图表的工具，常用于Markdown文件中，可以生成各种类型的图，包括类图、流程图、序列图等。

______________________________________________________________

## 目录
- [目录](#目录)
- [使用尖括号](#使用尖括号)
- [流程图](#流程图)
  - [流程图 参考1上下  `TD`](#流程图-参考1上下--td)
  - [流程图 参考2左右  `LR`](#流程图-参考2左右--lr)
- [树形图](#树形图)
  - [树形图 参考1上下  `TD`](#树形图-参考1上下--td)
  - [树形图 参考2左右  `LR`](#树形图-参考2左右--lr)
- [类图](#类图)
  - [类图参考1上下  `TB`](#类图参考1上下--tb)
  - [类图参考2左右  `LR`](#类图参考2左右--lr)



______________________________________________________________

## 使用尖括号

[使用尖括号需要HTML转义_这里是csdn链接_转义对照表](https://blog.csdn.net/qq_27852041/article/details/87914729)

______________________________________________________________

## 流程图 
````
```mermaid
flowchart TD
    A[用户购买商品] --> B[商家确认订单]
    B --> C[订单发货]
    C --> D[用户确认收货]
    D --> E[返利申请]
    E --> F[系统审核]
    F --> G{审核通过吗?}
    G -->|是| H[发放返利]
    G -->|否| I[拒绝返利]
    I --> J[通知用户]
    H --> A[用户购买商品]
```
````

### 流程图 参考1上下  `TD` 
```mermaid
flowchart TD
    A[用户购买商品] --> B[商家确认订单]
    B --> G{审核通过吗?}
    G -->|是| H[发放返利]
    G -->|否| I[拒绝返利]
    I --> B
    H --> A[用户购买商品]
```

### 流程图 参考2左右  `LR` 
```mermaid
flowchart LR
    A[用户购买商品] --> B[商家确认订单]
    B --> C[订单发货]
    C --> D[用户确认收货]
    D --> E[返利申请]
    E --> F[系统审核]
    F --> G{审核通过吗?}
    G -->|是| H[发放返利]
    G -->|否| I[拒绝返利]
    I --> J[通知用户]
    H --> A[用户购买商品]
```

______________________________________________________________

## 树形图 

```mermaid
graph LR;

    A[AuraEnemy中]-->|BeginPlay时调用|B[InitAbilityActorInfo函数];
    
    B--调用-->C[InitializeDefaultAttributes函数];
    
    subgraph "在基类中创建的函数"
        C[InitializeDefaultAttributes函数]  
    end
```


```mermaid
---
title: 这是一个标题
---
graph LR;
	A[ 11111 ]-->B[ 22222 ]
	B-->C[ 33333 ]
	
	subgraph "XXX"
		A
	end
	
	subgraph "XXX"
		B
	end
	
	subgraph "XXX"
		C
	end
```



````
```mermaid
---
title: 这是一个标题
---
graph LR;
	A[ 11111 ]-->B[ 22222 ]
	B-->C[ 33333 ]
	
	subgraph "XXX"
		A
	end
	
	subgraph "XXX"
		B
	end
	
	subgraph "XXX"
		C
	end
```
````

### 树形图 参考1上下  `TD` 

```mermaid
graph TD;
    Content-->BP;
    BP-->AbilitySystem;
    AbilitySystem-->GameplayEffects;
    GameplayEffects-->DefaultAttributes;
    DefaultAttributes-->Aura;
    DefaultAttributes-->Enemy;
    DefaultAttributes-->GE_SecondaryAttributes;
    DefaultAttributes-->GE_VitalAttributes;
    Aura-->GE_AuraPrimaryAttributes;
    Enemy-->GE_PrimaryAttributes_Warrior;
    Enemy-->GE_PrimaryAttributes_Ranger;
    Enemy-->GE_PrimaryAttributes_Elementalist;
```
### 树形图 参考2左右  `LR` 

```mermaid
graph LR;
    Content-->BP;
    BP-->AbilitySystem;
    AbilitySystem-->GameplayEffects;
    GameplayEffects-->DefaultAttributes;
    DefaultAttributes-->Aura;
    DefaultAttributes-->Enemy;
    DefaultAttributes-->GE_SecondaryAttributes;
    DefaultAttributes-->GE_VitalAttributes;
    Aura-->GE_AuraPrimaryAttributes;
    Enemy-->GE_PrimaryAttributes_Warrior;
    Enemy-->GE_PrimaryAttributes_Ranger;
    Enemy-->GE_PrimaryAttributes_Elementalist;
```




______________________________________________________________

## 类图


```mermaid
---
title: 这里是标题
---
classDiagram
direction TB
    class FloatText {
        +Overlay /*UI组件*/
        +Text_Damage /*文本块*/
        +DamageAnim /*动画*/
        +PlayAnimation() /*调用动画*/
    }

    class DamageTextComponent {
        <<abstract>>
        +SetDamageText(Damage float)/*设置伤害文本*/
    }

    class BP_DamageTextComponent {
        +UpdateDamageText(Damage float) /*更新伤害文本*/
        +SetDamageText(Damage float) /*实现伤害文本设置*/
    }

    class AAuraPlayerController {
        -TSubclassOf&lt;UDamageTextComponent&gt DamageTextComponentClass
        +ShowDamageNumber()/*RPC_Client事件显示伤害数字*/
    }

    class UAuraAttributeSet {
        -ShowFloatingText(FEffectProperties Props, Damage float) /*显示浮动文本*/
    }

    AAuraPlayerController --> DamageTextComponent : 创建
    AAuraPlayerController --> UAuraAttributeSet : 调用
    DamageTextComponent <|-- BP_DamageTextComponent : 继承
    FloatText --> BP_DamageTextComponent : 使用
    AAuraPlayerController --> FloatText : 使用
```

````
```mermaid
---
title: 这里是标题
---
classDiagram
direction TB
    class FloatText {
        +Overlay /*UI组件*/
        +Text_Damage /*文本块*/
        +DamageAnim /*动画*/
        +PlayAnimation() /*调用动画*/
    }

    class DamageTextComponent {
        <<abstract>>
        +SetDamageText(Damage float)/*设置伤害文本*/
    }

    class BP_DamageTextComponent {
        +UpdateDamageText(Damage float) /*更新伤害文本*/
        +SetDamageText(Damage float) /*实现伤害文本设置*/
    }

    class AAuraPlayerController {
        -TSubclassOf&lt;UDamageTextComponent&gt DamageTextComponentClass
        +ShowDamageNumber()/*RPC_Client事件显示伤害数字*/
    }

    class UAuraAttributeSet {
        -ShowFloatingText(FEffectProperties Props, Damage float) /*显示浮动文本*/
    }

    AAuraPlayerController --> DamageTextComponent : 创建
    AAuraPlayerController --> UAuraAttributeSet : 调用
    DamageTextComponent <|-- BP_DamageTextComponent : 继承
    FloatText --> BP_DamageTextComponent : 使用
    AAuraPlayerController --> FloatText : 使用
```
````


______________________________________________________________

### 类图参考1上下  `TB` 

```mermaid
classDiagram
direction TB
    class ULevel {
        TArray&lt;AActor*&gt; Actors
        ALevelScriptActor* LevelScriptActor
        TArray&lt;UModelComponent*&gt; ModelComponents
        AWorldSettings* WorldSettings;(Actors[0])
    }

    class AActor {
        TSet&lt;UActorComponent*&gt; OwnedComponents
        USceneComponent* RootComponent
        void Tick(float DeltaSeconds)
        TArray&lt;AActor*&gt; Children
        AActor* Owner;(weak)
        TSet&lt;UActorComponent*&gt; ReplicatedComponents
        TArray&lt;UActorComponent*&gt; InstanceComponents
        UInputComponent* InputComponent
    }

    class ALevelScriptActor {
        uint32 bInputEnabled:1
    }

    class AInfo {
        UBillboardComponent* SpriteComponent
    }

    class AWorldSettings {
        TSubclassOf&lt;class AGameMode&gt; DefaultGameMode
        Other settings
    }

    ULevel --> AActor
    ULevel --> ALevelScriptActor
    ULevel --> AWorldSettings
    AActor <|--- ALevelScriptActor
    AActor <|-- AInfo
    AInfo <|-- AWorldSettings



```

______________________________________________________________

### 类图参考2左右  `LR` 

```mermaid
classDiagram
direction LR
    class ULevel {
        TArray&lt;AActor*&gt; Actors
        ALevelScriptActor* LevelScriptActor
        TArray&lt;UModelComponent*&gt; ModelComponents
        AWorldSettings* WorldSettings;(Actors[0])
    }

    class AActor {
        TSet&lt;UActorComponent*&gt; OwnedComponents
        USceneComponent* RootComponent
        void Tick(float DeltaSeconds)
        TArray&lt;AActor*&gt; Children
        AActor* Owner;(weak)
        TSet&lt;UActorComponent*&gt; ReplicatedComponents
        TArray&lt;UActorComponent*&gt; InstanceComponents
        UInputComponent* InputComponent
    }

    class ALevelScriptActor {
        uint32 bInputEnabled:1
    }

    class AInfo {
        UBillboardComponent* SpriteComponent
    }

    class AWorldSettings {
        TSubclassOf&lt;class AGameMode&gt; DefaultGameMode
        Other settings
    }

    ULevel --> AActor
    ULevel --> ALevelScriptActor
    ULevel --> AWorldSettings
    AActor <|--- ALevelScriptActor
    AActor <|-- AInfo
    AInfo <|-- AWorldSettings



```

______________________________________________________________

