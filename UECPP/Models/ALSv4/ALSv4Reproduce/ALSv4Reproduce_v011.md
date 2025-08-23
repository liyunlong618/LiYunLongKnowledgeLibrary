
------

#### [返回菜单](../ALS_Menu.md)

------

# ALSv4复刻v011 Tikc组相关和显式确立Tick时序

------

## 目录

[TOC]

------

<details>
<summary>视频链接</summary>

> [高级运动系统解耦和复刻第十一期_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ja41197XQ?share_source=copy_web&vd_source=ccfefcf8d65f5d070c57cddf34c94047&spm_id_from=333.788.player.switch&p=14)

------

</details>

------

## 角色基类的`OnBeginPlay`中调用`SkeletamMesh`的`AddTickPrerequisiteActor`方法

`UActorComponent::AddTickPrerequisiteActor`的作用是：确保**`当前组件`**的 `Tick`函数在**`指定Actor`**的 `Tick`函数之后 执行




<details>
<summary>源码部分</summary>

> **为什么需要这个`UActorComponent::AddTickPrerequisiteActor`？**
>
> 想象一个常见的场景：你有一个 `Character`（Actor）和一个挂在他身上的 `WeaponComponent`（UActorComponent）。`Character`的 `Tick`会处理移动、输入等，计算出这一帧最终的位置和旋转。而 `WeaponComponent`的 `Tick`需要根据 `Character`最终的位置和旋转来更新武器模型的位置（比如进行插值、抵消摄像机抖动等）。
>
> 如果执行顺序反过来，`WeaponComponent`先用上一帧的 `Character`数据更新了自己，然后 `Character`才计算本帧的新位置。那么武器就会落后一帧，永远无法与角色完全同步，导致肉眼可见的抖动或延迟。`AddTickPrerequisiteActor`就是用来解决这种依赖关系的。
>
> ```CPP
> // ActorComponent.h
> void UActorComponent::AddTickPrerequisiteActor(AActor* PrerequisiteActor)
> {
>  // 检查了前提Actor有效且自身可以Tick后，调用了前提Actor的 PrimaryActorTick属性的 AddPrerequisite方法。
>  if (PrimaryComponentTick.bCanEverTick && PrerequisiteActor && PrerequisiteActor->PrimaryActorTick.bCanEverTick)
>  {
>     // 这里的 PrimaryActorTick 和 PrimaryComponentTick 都是 FTickFunction类型的对象。FTickFunction是虚幻引擎Tick系统的核心
>     PrimaryComponentTick.AddPrerequisite(PrerequisiteActor, PrerequisiteActor->PrimaryActorTick);
>  }
> }
> 
> // TickTaskManager.cpp
> void FTickFunction::AddPrerequisite(UObject* TargetObject, struct FTickFunction& TargetTickFunction)
> {
> 	const bool bThisCanTick = (bCanEverTick || IsTickFunctionRegistered());
> 	const bool bTargetCanTick = (TargetTickFunction.bCanEverTick || TargetTickFunction.IsTickFunctionRegistered());
> 
> 	if (bThisCanTick && bTargetCanTick)
> 	{
> 		Prerequisites.AddUnique(FTickPrerequisite(TargetObject, TargetTickFunction));
> 	}
> }
> ```
>
> #### FTickFunction 是什么？
>
> `FTickFunction`是一个结构体，它封装了所有被Tick的事物的信息：比如：`AActor`中`FActorTickFunction`类型的成员变量`PrimaryActorTick`
>
> - **PrerequisiteObject:** 实际被调用的对象，相当于TickTarget（如一个UActorComponent或AActor）。
> - **ExecuteTick:** 一个函数指针，指向真正的Tick函数（如 `AActor::TickActor`或 `UActorComponent::TickComponent`）。
> - **TickGroup:** 它属于哪个Tick组（如TG_PrePhysics, TG_DuringPhysics, TG_PostPhysics等）。这是第一层排序依据。
> - **PrerequisiteTickFunctions:** 一个 `TArray<FTickFunction*>`，存储了**必须在本次Tick之前执行**的所有其他TickFunction。
> - **PrerequisiteTickDependencies:** 另一个 `TArray<FTickFunction*>`，存储了**依赖于本次Tick**的所有其他TickFunction（即本次Tick是它们的Prerequisite）。
>
> ### 这里放一下`TickingGroup`相关的源码
>
> ```cpp
> /** Determines which ticking group a tick function belongs to. */
> UENUM(BlueprintType)
> enum ETickingGroup : int
> {
>     /** Any item that needs to be executed before physics simulation starts. */
>     TG_PrePhysics UMETA(DisplayName="Pre Physics"),
> 
>     /** Special tick group that starts physics simulation. */                    
>     TG_StartPhysics UMETA(Hidden, DisplayName="Start Physics"),
> 
>     /** Any item that can be run in parallel with our physics simulation work. */
>     TG_DuringPhysics UMETA(DisplayName="During Physics"),
> 
>     /** Special tick group that ends physics simulation. */
>     TG_EndPhysics UMETA(Hidden, DisplayName="End Physics"),
> 
>     /** Any item that needs rigid body and cloth simulation to be complete before being executed. */
>     TG_PostPhysics UMETA(DisplayName="Post Physics"),
> 
>     /** Any item that needs the update work to be done before being ticked. */
>     TG_PostUpdateWork UMETA(DisplayName="Post Update Work"),
> 
>     /** Catchall for anything demoted to the end. */
>     TG_LastDemotable UMETA(Hidden, DisplayName = "Last Demotable"),
> 
>     /** Special tick group that is not actually a tick group. After every tick group this is repeatedly re-run until there are no more newly spawned items to run. */
>     TG_NewlySpawned UMETA(Hidden, DisplayName="Newly Spawned"),
> 
>     TG_MAX,
> };
> ```
>
> 可以看到分为了**8个Tick组**
>
> | 组名 (ENUM)             | 中文名           | 时机与描述                                                   | 典型用途                                                     |
> | :---------------------- | :--------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
> | **`TG_PrePhysics`**     | **物理前更新**   | **在物理模拟开始之前执行。** 这是最早的可用于游戏逻辑的Tick组。 | 处理玩家输入、计算移动意图、进行非物理性的移动（如飞行、游泳）、AI决策。任何需要影响物理系统的逻辑都应放在这里。 |
> | **`TG_StartPhysics`**   | **物理开始**     | **标志着物理模拟阶段的开始。** 注意：**这个组通常不用于游戏逻辑Tick。** 它主要用于引擎内部启动物理模拟任务。用户自定义的Tick函数极少注册到这个组。 | 引擎内部使用。                                               |
> | **`TG_DuringPhysics`**  | **物理中更新**   | **与物理模拟并行执行。** 这是最需要小心使用的组。它的Tick函数**不保证**在物理模拟的某个精确点运行，因为它们是在另一个线程上并行处理的。 | 那些与物理模拟没有严格先后顺序、可以并行执行的非关键逻辑。对性能敏感且可并行的计算。**通常不建议常规游戏逻辑使用。** |
> | **`TG_EndPhysics`**     | **物理结束**     | **标志着物理模拟阶段的结束。** 与 `TG_StartPhysics`类似，**这个组通常也不用于游戏逻辑Tick**，而是引擎内部用于完成物理模拟。 | 引擎内部使用。                                               |
> | **`TG_PostPhysics`**    | **物理后更新**   | **在物理模拟完全完成之后执行。** 这是最常用、最安全的组之一。此时，所有物体的物理状态（位置、旋转、速度等）都已经计算完毕，是本帧的最终结果。 | 基于物理结果的逻辑：摄像机碰撞检测、武器附着、动画状态更新（需要最终位置）、触发器等。 |
> | **`TG_PostUpdateWork`** | **后期更新**     | **在 `TG_PostPhysics`之后执行。** 用于处理那些需要最终变换数据的逻辑。 | 摄像机管理（计算最终的视图矩阵）、UI元素的世界空间投射、绘制调试信息。 |
> | **`TG_LastDemotable`**  | **最终更新**     | **在 `TG_PostUpdateWork`之后，但在渲染线程开始处理本帧数据之前执行。** 这是游戏线程能处理本帧逻辑的**最后机会**。 | 非常晚期的、必须在渲染前完成的逻辑。例如，某些特殊的特效系统或自定义的渲染数据准备。 |
> | **`TG_NewlySpawned`**   | **新生对象更新** | **这是一个特殊的组。** 它**不是**一个标准的时序点。被标记为此组的Tick函数会被**降级（Demoted）** 到下一个合适的、更晚的TickGroup中去执行（通常是当前帧的 `TG_LastDemotable`）。**目的是保证新生成的对象不会在当前帧Tick。** | 确保通过 `SpawnActor`在当前帧创建的Actor，其 `Tick`函数会在**下一帧**才第一次执行，避免使用未完全初始化的状态。 |
>
> ## `AddPrerequisite(UActorComponent* DependentComponent, FTickFunction& DependentTickFunction)`的内部逻辑简化如下：
>
> 1. 找到 `PrerequisiteActor`（前提）的 `PrimaryActorTick`（一个 `FTickFunction`）。
> 2. 找到 `DependentComponent`（当前组件）的 `PrimaryComponentTick`（另一个 `FTickFunction`）。
> 3. 调用 `PrerequisiteActor->PrimaryActorTick.PrerequisiteTickDependencies.AddUnique(&DependentTickFunction)`
>    - **这意味着：** 将“当前组件的TickFunction”添加到“前提Actor的TickFunction”的“依赖我的人”的列表中。
> 4. 调用 `DependentComponent->PrimaryComponentTick.PrerequisiteTickFunctions.AddUnique(&PrerequisiteActor->PrimaryActorTick)`。
>    - **这意味着：** 将“前提Actor的TickFunction”添加到“当前组件的TickFunction”的“我必须等待的人”的列表中。
>
> **这样就建立了一个双向的依赖关系图。**
>
> 
>
> ## 引擎如何利用这个依赖图进行调度？
>
> Tick的调度发生在 `UGameEngine::Tick`中，最终会调用到 `FTickTaskManager`。
>
> 整个过程分为多个阶段：
>
> **阶段一：注册和收集（Register）**
>
> - 所有可Tick的Actor和Component都会将自己的 `FTickFunction`注册到全局的 `FTickTaskManager`中。
>
> **阶段二：并行化分析和排序（PreTick / Tick）**
>
> - 引擎并不是简单地把所有TickFunction扔进一个数组然后遍历。为了最大化利用多核CPU，它采用了**TaskGraph** 系统。
> - `FTickTaskManager`会遍历所有注册的TickFunction，并根据它们的 **TickGroup** 和 **Prerequisite依赖关系** 来构建一个**有向无环图（DAG）**。
> - **TickGroup是第一级排序：** 所有TG_PrePhysics的Tick都会在TG_DuringPhysics之前执行，以此类推。
> - **Prerequisite是第二级（组内）排序：** 在同一个TickGroup内部，依赖关系决定了执行顺序。如果A依赖B，那么B一定排在A之前。引擎会使用**拓扑排序（Topological Sort）** 算法来解析这个依赖图，找到一个合法的线性执行序列。
>
> **阶段三：分发和执行（Dispatch）**
>
> - 排序完成后，引擎不会自己按顺序调用每个TickFunction。
> - 它会将排好序的TickFunction列表转换成一系列**任务（Task）**，然后将这些任务投递到**任务图系统**中。
> - 任务图系统的工作线程会从任务队列中领取任务并执行。**关键点在于：** 任务之间的依赖关系（通过 `PrerequisiteTickFunctions`建立）会被翻译成任务图的“前置任务（Prerequisite Task）”。一个任务只有在它的所有前置任务都完成后，才会被允许执行。
> - 这就是为什么即使你的 `WeaponComponent`和 `Character`在同一个TickGroup（比如TG_PrePhysics），并且被不同的线程处理，依赖关系也依然能保证正确。线程在准备执行 `WeaponComponent`的Tick任务时，会先检查其前置任务（`Character`的Tick）是否已完成。如果没完成，它就等待或先去处理其他任务。
>
> **阶段四：收尾（PostTick）**
>
> - 所有TickGroup都处理完毕后，进入下一帧。
>
> ### 总结与工作流程
>
> 当你调用 `MyWeaponComponent->AddTickPrerequisiteActor(MyCharacter)`时，你实际上是在做：
>
> 1. **声明依赖：** “MyWeaponComponent的Tick依赖于MyCharacter的Tick”。
> 2. **修改图结构：** 在引擎内部的Tick依赖图中添加了一条从 `MyCharacter->PrimaryActorTick`指向 `MyWeaponComponent->PrimaryComponentTick`的边。
> 3. **影响调度：** 在每一帧的Tick调度阶段，任务图系统会识别这条边，并确保 `MyCharacter`的Tick任务作为 `MyWeaponComponent`的Tick任务的前置任务。
> 4. **保证顺序：** 最终，无论在单线程还是多线程环境下，`MyCharacter->Tick()`总是先于 `MyWeaponComponent->TickComponent()`执行。
>
> ## 那如果，我在运行时创建了一个Actor，比如GetWorld->SpawnActor出来的，那它会加到哪个Tick组？根据父类吗？还是直接走默认值？那Tick顺序呢？排在谁的后面，谁的前面，这个如何确定？
>
> TickGroup，通常来自CDO（Class Default Object）
>
> 生成时是否允许Tick也很关键，因为bCanEverTick和bStartWithTickEnabled会影响是否注册到调度系统
>
> Tick顺序的确定，除了Tick组，还有注册顺序和依赖关系。新Actor在生成时注册，会排在当前帧已注册Actor之后，但如果有依赖关系，任务图会通过拓扑排序处理
>
> ### 简述一下答案：加到哪个组会根据创建时的参数`PrimaryActorTick`和CDO决定，Tick顺序会优先根据TickGroup排序，然后会根据注册顺序决定当前组内的顺序（排在队尾）
>
> ### 1. TickGroup 的确定：继承与默认值
>
> 当一个Actor通过 `UWorld::SpawnActor`被创建时，它的 `PrimaryActorTick`属性（这是一个 `FTickFunction`）的 `TickGroup`是如何确定的？
>
> **来自于该Actor类的类默认对象（CDO - Class Default Object）。**
>
> - **CDO 是什么？** 每个UClass都有一个单例对象，称为CDO，它存储了该类的所有属性的默认值。当你编译C++代码或蓝图时，这些默认值就被确定了。
> - **初始化流程：**
>   1. `SpawnActor`会创建Actor的一个新实例。
>   2. 在构造过程中，这个新实例的属性的初始值会**从CDO复制过来**。这包括了 `PrimaryActorTick`这个结构体中的所有成员，自然也就包括了 `TickGroup`。
>   3. 因此，一个新生的Actor，它的TickGroup**完全由其所属的类决定**。你在蓝图或C++中为这个类设置的默认TickGroup是什么，生成出来的Actor就是什么。
>
> **如何设置默认TickGroup？**
>
> - **C++:** 在类的构造函数中设置。
>
>   ```cpp
>   AMyActor::AMyActor()
>   {
>       PrimaryActorTick.TickGroup = TG_PostPhysics; // 例如设置为物理后更新
>       PrimaryActorTick.bCanEverTick = true;
>       // ...
>   }
>   ```
>
> - **蓝图:** 在蓝图的“细节”面板中，“Actor”分类下直接设置“Tick Group”属性。
>
> **结论：** 运行时生成的Actor，其TickGroup**直接走CDO中的默认值**，与“父类”无关（除非父类构造函数修改了它，但那是初始化逻辑，不是继承关系）。
>
> ------
>
> ### 2. Tick 顺序的确定：一个多层次的排序系统
>
> “排在谁的后面，谁的前面”这个问题更复杂，它不是一个简单的列表，而是一个由**多个层级规则**共同决定的系统。引擎每一帧都会为所有需要Tick的Actor和组件计算出一个执行顺序。
>
> 决定顺序的规则，按优先级从高到低排列：
>
> #### 第一级：TickGroup（最高优先级）
>
> 这是最粗粒度的排序。引擎会严格按照TickGroup的枚举顺序进行Tick。顺序是：
>
> ```
> TG_PrePhysics`-> `TG_DuringPhysics`-> `TG_PostPhysics`-> `TG_PostUpdateWork`-> `TG_LastDemotable
> ```
>
> **规则：** 所有在 `TG_PrePhysics`组的Actor一定会在所有 `TG_DuringPhysics`组的Actor**之前**完成Tick。这是绝对的，无法被逾越的鸿沟。
>
> #### 第二级：依赖关系（Prerequisite Dependencies）
>
> **在同一个TickGroup内部**，顺序由我们之前讨论的**依赖关系图**决定。
>
> - 如果Actor A的Tick是Actor B的Tick的 prerequisite（通过 `AddTickPrerequisiteActor`设置），那么**无论注册顺序如何**，A的Tick一定会排在B的Tick之前执行。
> - 引擎使用拓扑排序算法来解析这个依赖图，保证依赖者永远在被依赖者之后执行。
>
> #### 第三级：注册顺序（Fallback）
>
> **在同一个TickGroup内部，且彼此之间没有建立任何依赖关系**的Actor们，它们的执行顺序就由**注册顺序**决定。
>
> - **“注册”是什么意思？** 当一个Actor的 `bCanEverTick`为true且 `bStartWithTickEnabled`为true（或之后被激活）时，它会在某一帧将自己注册到全局的Tick任务管理器中。
> - **新生成的Actor何时注册？** `SpawnActor`调用通常发生在某帧的GameThread逻辑中（例如在某个Actor的Tick里生成新Actor）。这个新Actor会在**当前帧的Tick注册阶段结束时**被加入到注册列表里。
> - **顺序如何？** 对于在同一帧中生成的多个Actor，它们的注册顺序通常与生成（Spawn）的调用顺序一致。
>
> **因此，对于一个新生Actor：**
>
> 1. 它会被排在它**所在TickGroup的队列末尾**。
> 2. 如果这个组里已经有100个老Actor，那么新Actor就会排在第101位。
> 3. 它会在这个组内所有老Actor之后、但在下一TickGroup的所有Actor之前执行Tick。
>
> ------
>
> ### 总结与工作流程模拟
>
> 假设你在第N帧的 `TG_DuringPhysics`阶段（例如某个Character的Tick函数里）调用 `SpawnActor`生成了一个 `Actor_X`，它的默认TickGroup也是 `TG_DuringPhysics`。
>
> 1. **生成（Spawn）：** `Actor_X`被创建，其 `PrimaryActorTick.TickGroup`被设置为 `TG_DuringPhysics`。
> 2. **注册（Register）：** 在第N帧的Tick注册阶段结束时，`Actor_X`被添加到 `FTickTaskManager`中 `TG_DuringPhysics`组的**注册列表的末尾**。
> 3. **排序（Sort）：** 在第N+1帧的Tick开始前：
>    - **第一级：** 引擎先处理完所有 `TG_PrePhysics`的Actor。
>    - **第二级：** 开始处理 `TG_DuringPhysics`组。引擎会先根据**依赖关系**对这个组内的所有Actor（包括老Actor和`Actor_X`）进行拓扑排序，修正它们的顺序。如果 `Actor_X`被一个老Actor依赖，它可能会被排到前面去。
>    - **第三级：** 对于没有依赖关系的Actor，保持它们的**注册顺序**。因为 `Actor_X`是上一帧末尾新注册的，所以它通常排在这个组所有“资深”Actor的后面。
> 4. **执行（Execute）：** 在第N+1帧，`Actor_X`的 `Tick`函数会在其TickGroup内、所有没有依赖它的老Actor之后执行。
>
> **给你的实践建议：**
>
> - **不要依赖注册顺序！** 这是最脆弱的一种顺序保证。不同平台、不同优化下的执行顺序可能产生差异。
> - 如果两个Actor的逻辑有严格的先后要求，**永远优先使用 `AddTickPrerequisiteActor`或 `AddTickPrerequisiteComponent`来显式地建立依赖关系**。这是唯一可靠的方法。
> - 合理地设置 `TickGroup`是优化性能和保证逻辑正确性的重要手段。例如，不需要物理信息的特效放在 `TG_PostPhysics`，需要根据最终位置渲染的物品放在 `TG_LastDemotable`。

------

</details>




------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

## XXXXXXXXXXXXX

xxxxxxxxxxxxxxxxxxxxxxxx

------

XXXXXXXXXXXXX
------

[返回最上面](#返回菜单)

___________________________________________________________________________________________
