
___________________________________________________________________________________________

# 思路流程/概念理解
___________________________________________________________________________________________
>(整理中)
___________________________________________________________________________________________
# 目录

- [操作相关：关键点梳理](#操作相关关键点梳理)
        - [处理关键点](#处理关键点)
          - [1. 再C++中使用FName插槽名，将武器SK，绑定到角色SK上](#1-再c中使用fname插槽名将武器sk绑定到角色sk上)
          - [2. 使用动画蓝图模板](#2-使用动画蓝图模板)
        - [处理关键点](#处理关键点-1)
          - [1. PlayerController配置鼠标相关设置](#1-playercontroller配置鼠标相关设置)
          - [2. PlayerController配置增强输入](#2-playercontroller配置增强输入)
          - [3. 增强输入配置](#3-增强输入配置)
          - [4. 增强输入移动形参类型](#4-增强输入移动形参类型)
          - [5. PlayerController的角色移动旋转计算](#5-playercontroller的角色移动旋转计算)
          - [6. 转身速率配置](#6-转身速率配置)
          - [7. PlayerControllerRotation映射SpringArm旋转配置](#7-playercontrollerrotation映射springarm旋转配置)
        - [处理关键点](#处理关键点-2)
          - [1. 接口Interface的使用（比如权限和纯虚函数）](#1-接口interface的使用比如权限和纯虚函数)
          - [2. PlayerController中使用 获取鼠标的位置发射射线，返回结果 的函数（只识别block）](#2-playercontroller中使用-获取鼠标的位置发射射线返回结果-的函数只识别block)
          - [3. 自定义边缘发光深度材质 生效相关配置（Post Process Volume生效范围/后期处理材质配置）](#3-自定义边缘发光深度材质-生效相关配置post-process-volume生效范围后期处理材质配置)
          - [4. 在项目文件中定义宏并使用](#4-在项目文件中定义宏并使用)
        - [处理关键点](#处理关键点-3)
          - [1. 角色PS中创建ASC组件,角色通过PS持有ASC组件和AS组件](#1-角色ps中创建asc组件角色通过ps持有asc组件和as组件)
          - [2. 调用ASC组件的初始化函数进行初始化（不能在构造中初始化！）](#2-调用asc组件的初始化函数进行初始化不能在构造中初始化)
          - [3. ASC组件——网络复制 属性同步模式,一共有3种类型:1.Minimal /2.Mixed /3.Full](#3-asc组件网络复制-属性同步模式一共有3种类型1minimal-2mixed-3full)
          - [4. 当PlayerState存在时 同步给所有客户端 的函数](#4-当playerstate存在时-同步给所有客户端-的函数)
        - [处理关键点](#处理关键点-4)
          - [1. GetLifetimeReplicatedProps 此函数在U0bject中 开启 属性复制(RepNotify)后 需要重写这个函数!//此函数规定了:1.哪些参数同步 以及 2.同步的条件](#1-getlifetimereplicatedprops-此函数在u0bject中-开启-属性复制repnotify后-需要重写这个函数此函数规定了1哪些参数同步-以及-2同步的条件)
          - [2. 根据AttributeSet基类中写好的宏Get/set/lnit 属性；](#2-根据attributeset基类中写好的宏getsetlnit-属性)
          - [3. 为每个属性创建属性复制和相关函数；调用同步函数,设置同步参数；DOREPLIFETIME\_CONDITION\_NOTIFY宏使用（在UnrealNetwork.h中）](#3-为每个属性创建属性复制和相关函数调用同步函数设置同步参数doreplifetime_condition_notify宏使用在unrealnetworkh中)
        - [处理关键点](#处理关键点-5)
          - [下面是结构梳理：](#下面是结构梳理)
          - [1 MVC(Model-\>四大数据PC/PS/ASC/AS；](#1-mvcmodel-四大数据pcpsascas)
          - [2 View-\>AuraUserWidget；Control-\>WidgetController)+使用发布更新的架构](#2-view-aurauserwidgetcontrol-widgetcontroller使用发布更新的架构)
          - [3 1角色（这里是角色，也可以是别的）初始化时调用HUD，根据配置的class在堆区实例化OverlayWidgetController，](#3-1角色这里是角色也可以是别的初始化时调用hud根据配置的class在堆区实例化overlaywidgetcontroller)
          - [4 传入数据更新OverlayWidgetController中的数据（只在初始化时，创建包含四大数据的结构体，才给OverlayWidgetController传入指针数据，后续自行持有指针）](#4-传入数据更新overlaywidgetcontroller中的数据只在初始化时创建包含四大数据的结构体才给overlaywidgetcontroller传入指针数据后续自行持有指针)
        - [处理关键点](#处理关键点-6)
          - [1. 动态单播,在c++中声明,蓝图中绑定回调](#1-动态单播在c中声明蓝图中绑定回调)
          - [2. ASC组件 调用 获取属性变化委托,传入特定类型属性,且 回调函数形参 必须为const FOnAttributeChangeData类型](#2-asc组件-调用-获取属性变化委托传入特定类型属性且-回调函数形参-必须为const-fonattributechangedata类型)
        - [处理关键点](#处理关键点-7)
          - [1. 此函数使用 `UAbilitySystemBlueprintLibrary` 函数库中的API (检查目标是否实现了IAbilitySystemInterface 接口/若未实现 返回nullptr)](#1-此函数使用-uabilitysystemblueprintlibrary-函数库中的api-检查目标是否实现了iabilitysysteminterface-接口若未实现-返回nullptr)
          - [2. 道具类使用GE:](#2-道具类使用ge)
        - [处理关键点](#处理关键点-8)
          - [1. `AuraAttributeSet`中重写虚函数`PreAttributeChange`(属性更改前 预处理)限制属性最大最小值](#1-auraattributeset中重写虚函数preattributechange属性更改前-预处理限制属性最大最小值)
          - [2. 了解属性更改后 **处理虚函数** `PostGameplayEffectExecute`](#2-了解属性更改后-处理虚函数-postgameplayeffectexecute)
          - [3. 实参 `Data` ,几乎能拿到所有信息](#3-实参-data-几乎能拿到所有信息)
          - [4. **给GE数值配表**](#4-给ge数值配表)
        - [处理关键点](#处理关键点-9)
          - [1. 使用ASC组件基类中,写好的委托 `OnGameplayEffectAppliedDelegateToSelf`（当应用GE到ASC时触发回调）](#1-使用asc组件基类中写好的委托-ongameplayeffectapplieddelegatetoself当应用ge到asc时触发回调)
          - [2. 一次性道具 配置资产标签`AssetTag`,这样可以在触发回调时通过`FGameplayEffectSpec`类的对象拿到`FGameplayTagContainer`（这个相当于水杯,tag相当于水）](#2-一次性道具-配置资产标签assettag这样可以在触发回调时通过fgameplayeffectspec类的对象拿到fgameplaytagcontainer这个相当于水杯tag相当于水)
          - [3. 使用`GEngine->AddOnScreenDebugMessage`（相当于`PrintString`）发Message到视口](#3-使用gengine-addonscreendebugmessage相当于printstring发message到视口)
          - [4. 先创建表格结构体（需要继承`FTableRowBase`！！！）在创建模板类,根据传入的表格查找指定行（`FindRow`,这里行命名实用了tag字符串的格式,便于查找）](#4-先创建表格结构体需要继承ftablerowbase在创建模板类根据传入的表格查找指定行findrow这里行命名实用了tag字符串的格式便于查找)
          - [5. `UPROPERTY(EditDefaultOnly)`宏//在编辑器中显示并允许编辑这些属性的默认值,但不允许在实例级别进行修改。](#5-upropertyeditdefaultonly宏在编辑器中显示并允许编辑这些属性的默认值但不允许在实例级别进行修改)
          - [6. C++中创建Tag标签:`FGameplayTag::RequestGameplayTag(FName("Message"));`并使用API（父类标签包含子类标签前提下） :子类`Tag.MatchesTag`(父类Tag)检查子类标签中是否包含父类标签,若反过来检查则不生效,请注意！！！](#6-c中创建tag标签fgameplaytagrequestgameplaytagfnamemessage并使用api父类标签包含子类标签前提下-子类tagmatchestag父类tag检查子类标签中是否包含父类标签若反过来检查则不生效请注意)
        - [处理关键点](#处理关键点-10)
          - [1. 重写后处理函数PostGameplayEffectExecute,使用clamp限制](#1-重写后处理函数postgameplayeffectexecute使用clamp限制)
        - [处理关键点](#处理关键点-11)
          - [1. 初始化属性的三种方法](#1-初始化属性的三种方法)
        - [处理关键点](#处理关键点-12)
          - [1. 属性同步 配置](#1-属性同步-配置)
          - [2. UE inline宏 `FORCEINLINE`](#2-ue-inline宏-forceinline)
        - [处理关键点](#处理关键点-13)
          - [1. 自定义属性计算方式需要创建类`GameplayModMagnitudecalculation`](#1-自定义属性计算方式需要创建类gameplaymodmagnitudecalculation)
        - [处理关键点](#处理关键点-14)
          - [1. 创建无类型的纯C++类,创建用于管理GameplayTags的结构体FAuraGameplayTags,创建初始化游戏标签函数,私有时声明一个变量,在源文件中定义](#1-创建无类型的纯c类创建用于管理gameplaytags的结构体fauragameplaytags创建初始化游戏标签函数私有时声明一个变量在源文件中定义)
          - [2. 单例类的变量使用（static）](#2-单例类的变量使用static)
          - [3. 创建自己的AssetManager类,提换引擎默认的资产管理器,重写虚函数StartInitialLoading,在加载完毕时,添加自己的逻辑（项目中的Config文件夹下的DefaultEngine.ini文件中查找(找不到就添加)设置自建的类型AuraAssetManager）](#3-创建自己的assetmanager类提换引擎默认的资产管理器重写虚函数startinitialloading在加载完毕时添加自己的逻辑项目中的config文件夹下的defaultengineini文件中查找找不到就添加设置自建的类型auraassetmanager)
        - [处理关键点](#处理关键点-15)
          - [1. `UFUNCTION(BlueprintPure,Category="AuraAbilitySystemLibrary|WidgetController",meta=(WorldContext="WorldContextObject"))`](#1-ufunctionblueprintpurecategoryauraabilitysystemlibrarywidgetcontrollermetaworldcontextworldcontextobject)
          - [2. 若形参中 有const UObject\* WorldContextObject这个作为世界上下文,上面的宏UFUNCTION(meta=(WorldContext="WorldContextObject")),可以自动识别函数的世界上下文](#2-若形参中-有const-uobject-worldcontextobject这个作为世界上下文上面的宏ufunctionmetaworldcontextworldcontextobject可以自动识别函数的世界上下文)
          - [3. 拿数据:PS从PC拿,ASC和AS从PS拿（因为在PS中创建）](#3-拿数据ps从pc拿asc和as从ps拿因为在ps中创建)
        - [处理关键点](#处理关键点-16)
          - [1. 模板函数的使用](#1-模板函数的使用)
          - [2. if constexpr 是一种条件编译语句,它允许在编译时进行条件检查,并且只有满足条件的分支代码会被编译。这与普通的 if 语句不同,普通的 if 语句是在运行时进行条件检查。示例:](#2-if-constexpr-是一种条件编译语句它允许在编译时进行条件检查并且只有满足条件的分支代码会被编译这与普通的-if-语句不同普通的-if-语句是在运行时进行条件检查示例)
        - [处理关键点](#处理关键点-17)
          - [1. 属性菜单发送多播,单独属性的ItemWidgetUI接收,验证tag一致后更新自身信息（使用MachesTag验证）](#1-属性菜单发送多播单独属性的itemwidgetui接收验证tag一致后更新自身信息使用machestag验证)
          - [2. 使用TMap把类型变量与静态函数的函数指针进行绑定](#2-使用tmap把类型变量与静态函数的函数指针进行绑定)
          - [](#)
          - [3. 函数指针格式`返回值类型（*指针名称）（参数类型）`](#3-函数指针格式返回值类型指针名称参数类型)
          - [4. 函数指针使用时格式:`函数指针名();`即可调用](#4-函数指针使用时格式函数指针名即可调用)
          - [5. 通过ASC组件获取 当属性变化时广播的委托变量/绑定Lambda回调](#5-通过asc组件获取-当属性变化时广播的委托变量绑定lambda回调)
        - [处理关键点](#处理关键点-18)
          - [1. 只有服务器才能赋予技能](#1-只有服务器才能赋予技能)
          - [2. 学习技能时,先使用GA的Class创建FGameplayabilitySpec技能规范,然后调用API:`GiveAbilityAndActivateOnce`(这里传入技能规范)才能学习](#2-学习技能时先使用ga的class创建fgameplayabilityspec技能规范然后调用apigiveabilityandactivateonce这里传入技能规范才能学习)
        - [处理关键点](#处理关键点-19)
          - [1. 使用C++模板,创建了一个函数模板](#1-使用c模板创建了一个函数模板)
          - [2. 具体参考《C++模板》(书我的在微信收藏里)](#2-具体参考c模板书我的在微信收藏里)
        - [处理关键点](#处理关键点-20)
          - [1. 引擎中配置增强输入:`项目设置`-\>`输入`-\>`默认输入组件类`](#1-引擎中配置增强输入项目设置-输入-默认输入组件类)
        - [处理关键点](#处理关键点-21)
          - [1. 赋予角色技能时,给 技能GA 添加 动态标签DynamicAbilityTag](#1-赋予角色技能时给-技能ga-添加-动态标签dynamicabilitytag)
          - [2. 调用 ASC组件中的API: GetActivatableAbilities()可以拿到所以可以激活的GA的Spec](#2-调用-asc组件中的api-getactivatableabilities可以拿到所以可以激活的ga的spec)
          - [3. GA的Spec 中 有一个动态技能标签 DynamicAbilityTags 若技能激活时 会拥有该 Tag](#3-ga的spec-中-有一个动态技能标签-dynamicabilitytags-若技能激活时-会拥有该-tag)
          - [4. 调用 ASC组件中的API: `AbilitySpecInputPressed(AbilitySpec);`会 标记技能的输入状态为已按下](#4-调用-asc组件中的api-abilityspecinputpressedabilityspec会-标记技能的输入状态为已按下)
          - [5. 使用 ASC组件中的API: `TryActivateAbility(AbilitySpec.Handle);`尝试激活该技能 若激活技能 会把 `AbilitySpec` 标记为已激活 `IsActive`](#5-使用-asc组件中的api-tryactivateabilityabilityspechandle尝试激活该技能-若激活技能-会把-abilityspec-标记为已激活-isactive)
          - [6. 使用`AbilitySpec.Handle` 激活该技能`TryActivateAbility(AbilitySpec.Handle);`](#6-使用abilityspechandle-激活该技能tryactivateabilityabilityspechandle)
        - [处理关键点](#处理关键点-22)
          - [1. 了解官方俯视角游戏DS/LS框架下的问题](#1-了解官方俯视角游戏dsls框架下的问题)
          - [2. 梳理点击移动的逻辑](#2-梳理点击移动的逻辑)
        - [处理关键点](#处理关键点-23)
          - [1. 样条线API](#1-样条线api)
          - [2. 获取NaviMesh的导航路径NaviPath上的点](#2-获取navimesh的导航路径navipath上的点)
        - [处理关键点](#处理关键点-24)
          - [1. 优化逻辑步骤](#1-优化逻辑步骤)
          - [2. C++中的RPC](#2-c中的rpc)
        - [处理关键点](#处理关键点-25)
          - [1. C++构造中设置碰撞通道和类型](#1-c构造中设置碰撞通道和类型)
          - [2. C++构造中设置抛射物组件参数](#2-c构造中设置抛射物组件参数)
        - [处理关键点](#处理关键点-26)
          - [1. 只有服务器才能生成火球:](#1-只有服务器才能生成火球)
          - [2. GA中,使用API:`GetAvatarActorFromActorInfo` 拿到使用`该GA的Actor`](#2-ga中使用apigetavataractorfromactorinfo-拿到使用该ga的actor)
          - [3. GA中,使用API:`GetOwningActorFromActorInfo` 获取`Owner`](#3-ga中使用apigetowningactorfromactorinfo-获取owner)
          - [4. 使用 `GetWorld()->SpawnActorDeferred` `延时生成Actor`(延时生成还需要调用 `FinishSpawning` )](#4-使用-getworld-spawnactordeferred-延时生成actor延时生成还需要调用-finishspawning-)
          - [5. GA中通过`WaitGamePlayEvent`,接收事件的Tag,发送时使用`SendGameplayEventToActor`,发送事件Tag](#5-ga中通过waitgameplayevent接收事件的tag发送时使用sendgameplayeventtoactor发送事件tag)
        - [处理关键点](#处理关键点-27)
          - [1. UFUNCTION宏的一些用法](#1-ufunction宏的一些用法)
          - [2. `UAbilityTask`](#2-uabilitytask)
        - [处理关键点](#处理关键点-28)
          - [1. 梳理清楚GAS的`AbilityTask`中`TargetData`的网络同步,时间差异思路梳理:](#1-梳理清楚gas的abilitytask中targetdata的网络同步时间差异思路梳理)
          - [2. 通信需要发送 `FGameplayAbilityTargetDataHandle` 类型数据,如果需要区分数据类型,需要使用从`TargetData`派生的类,赋值并添加到`TargetDataHandle`中](#2-通信需要发送-fgameplayabilitytargetdatahandle-类型数据如果需要区分数据类型需要使用从targetdata派生的类赋值并添加到targetdatahandle中)
          - [3. GAS预测,看文档吧,太复杂](#3-gas预测看文档吧太复杂)
          - [4. 服务器接收时回调参数需要为 `const FGameplayAbilityTargetDataHandle& DataHandle, FGameplayTag ActivationTag`](#4-服务器接收时回调参数需要为-const-fgameplayabilitytargetdatahandle-datahandle-fgameplaytag-activationtag)
          - [5. 服务器接收流程:](#5-服务器接收流程)
        - [处理关键点](#处理关键点-29)
          - [1. 使用: `向量.Rotation();` 获取角度FRotator](#1-使用-向量rotation-获取角度frotator)
          - [2. 使用: `角度.Quaternion();` 获取该角度的四元数](#2-使用-角度quaternion-获取该角度的四元数)
          - [3. C++中设置 碰撞通道](#3-c中设置-碰撞通道)
          - [4. DS / LS网络复制相关](#4-ds--ls网络复制相关)
        - [处理关键点](#处理关键点-30)
          - [1. MotionWarping插件使用流程](#1-motionwarping插件使用流程)
        - [处理关键点](#处理关键点-31)
          - [1. 生成音频调用API: `UGameplayStatics::PlaySoundAtLocation;`生成音频绑定在目标身上API: `UGameplayStatics::SpawnSoundAttached` 此函数返回一个组件,可以使用 `.Stop();` 停止播放](#1-生成音频调用api-ugameplaystaticsplaysoundatlocation生成音频绑定在目标身上api-ugameplaystaticsspawnsoundattached-此函数返回一个组件可以使用-stop-停止播放)
          - [2. 使用Niagara粒子系统需要引模块`Niagara`](#2-使用niagara粒子系统需要引模块niagara)
          - [3. 生成Niagara粒子调用API: `UNiagaraFunctionLibrary::SpawnSystemAtLocation;`](#3-生成niagara粒子调用api-uniagarafunctionlibraryspawnsystematlocation)
          - [4. 重写`Destoryed`虚函数时,注意!!!要在`调用父函数之前`写逻辑!](#4-重写destoryed虚函数时注意要在调用父函数之前写逻辑)
        - [处理关键点](#处理关键点-32)
          - [1. 物体若要碰撞检测需要开启`Generate Overlap Events`](#1-物体若要碰撞检测需要开启generate-overlap-events)
          - [2. 当我们第一次创建自定义碰撞通道时,它会占用游戏追踪1"`ECC_GameTraceChannel1`"这个通道](#2-当我们第一次创建自定义碰撞通道时它会占用游戏追踪1ecc_gametracechannel1这个通道)
        - [处理关键点](#处理关键点-33)
          - [1. 火球携带的不是GE而是`FGameplayEffectSpecHandle`,方便直接使用](#1-火球携带的不是ge而是fgameplayeffectspechandle方便直接使用)
          - [2. 重温`初始化AttributeSet`的流程](#2-重温初始化attributeset的流程)

___________________________________________________________________________________________

1. ### [GAS 001 配置项目/设置Mesh/插槽/动画(创建和使用ABP模板)](./DetailContent/GAS_001.md)

2. ### [GAS 002 配置增强输入/GM/玩家移动/转身速率](./DetailContent/GAS_002.md)

3. ### [GAS 003 通过(接口)实现(描边)效果](./DetailContent/GAS_003.md)

4. ### [GAS 004 GAS网络同步的 属性同步模式 类型 和 设置](./DetailContent/GAS_004.md)

5. ### [GAS 005 设置属性；创建一个加血的血瓶](./DetailContent/GAS_005.md)

6. ### [GAS 006 创建UI](./DetailContent/GAS_006.md)

7. ### [GAS 007 项目MVC架构](./DetailContent/GAS_007.md)

8. ### [GAS 008 配置多播](./DetailContent/GAS_008.md)

9. ### [GAS 009 即时生效GE/持续时间内生效的GE(比如增益BUFF)/永久生效的GE/GE中的Stacking(效果堆叠)](./DetailContent/GAS_009.md)

10. ### [GAS 010 AttributeSet中限制HP/MP最大最小值:创建药水的表格](./DetailContent/GAS_010.md)

11. ### [GAS 011 什么是GameplayTags？:创建GameplayTags两种方式:给物体添加标签](./DetailContent/GAS_011.md)

12. ### [GAS 012 绑定GE委托,通过收到的的资产标签,广播信息结构体,触发UI中绑定的WidgetController回调,UI中拿到生成MessageUI的信息](./DetailContent/GAS_012.md)

13. ### [GAS 013 拾取道具的小UI:HP和MP的滞后效果](./DetailContent/GAS_013.md)

14. ### [GAS 014 配表 初始化属性:GE中的Modifiers中的Coefficient（简单属性计算）](./DetailContent/GAS_014.md)

15. ### [GAS 015 主要属性和次要属性设计](./DetailContent/GAS_015.md)

16. ### [GAS 016 创建和配置 主要属性和次要属性:初始化次要属性(使用简单公式)](./DetailContent/GAS_016.md)

17. ### [GAS 017 创建接口(查询对象的等级)](./DetailContent/GAS_017.md)

18. ### [GAS 018 MMC——Modifier Magnitude calculation(自定义属性计算方式);以及如何使用自定义后的值初始化HP/MP属性](./DetailContent/GAS_018.md)

19. ### [GAS 019 UI属性面板 显示/隐藏:创建通用按钮UI](./DetailContent/GAS_019.md)

20. ### [GAS 020 创建:1.管理游戏标签结构体;2.自己的资产管理器类;3.创建DataAsset资产:4.制作WidgetController](./DetailContent/GAS_020.md)

21. ### [GAS 021 创建蓝图函数库](./DetailContent/GAS_021.md)

22. ### [GAS 022 创建模板函数——抽象  UAuraAbilitySystemLibrary 里面获取WidgetController的部分](./DetailContent/GAS_022.md)

23. ### [GAS 023 重点！！！(委托绑定/变参函数模板)属性面板UI中绑定委托更新消息](./DetailContent/GAS_023.md)

24. ### [GAS 024 概念和联网 GA(GameplayAbilities)](./DetailContent/GAS_024.md)

25. ### [GAS 025 授予能力GA](./DetailContent/GAS_025.md)

26. ### [GAS 026 GameplayAbility中的Tag——技能互斥](./DetailContent/GAS_026.md)

27. ### [GAS 027 使用数据资产将 输入 与 输入触发的Tag 绑定](./DetailContent/GAS_027.md)

28. ### [GAS 028 创建自建增强输入组件,创建函数模板](./DetailContent/GAS_028.md)

29. ### [GAS 029 AAuraPlayerController中为自建增强输入组件创建并绑定按键回调,引擎中配置增强输入](./DetailContent/GAS_029.md)

30. ### [GAS 030 GA中配置Tag,并在按下和松开按键时的回调函数中设置,保证释放GA时,触发并持有该Tag](./DetailContent/GAS_030.md)

31. ### [GAS 031 PC实现点击移动_参考官方 俯视角游戏模板](./DetailContent/GAS_031.md)

32. ### [GAS 032 PC短按 实现自动移动](./DetailContent/GAS_032.md)

33. ### [GAS 033 人物沿样条线运动 获取NaviMesh的Path导航路径上的点](./DetailContent/GAS_033.md)

34. ### [GAS 034 优化PC中的逻辑 运行时勿重复获取结果 精简代码 考虑可能出现的bug](./DetailContent/GAS_034.md)

35. ### [GAS 035 创建抛射物类,蓝图继承并配置NS,替换地板](./DetailContent/GAS_035.md)

36. ### [GAS 036 创建新的C++类继承自UAuraGameplayAbility重写ActivateAbility虚函数打印测试](./DetailContent/GAS_036.md)

37. ### [GAS 037 GA中在服务器端生成火球](./DetailContent/GAS_037.md)

38. ### [GAS 038 使用自定义AbilityTasks](./DetailContent/GAS_038.md)

39. ### [GAS 039 Ability Task中的TargetData处理时间差异的方法流程思路](./DetailContent/GAS_039.md)

40. ### [GAS 040 gas中的预测,Ability Task中,Client端发送 鼠标点击数据的TargetData,并在Server端接收](./DetailContent/GAS_040.md)

41. ### [GAS 041 预测和预测密钥Predictionkey梳理](./DetailContent/GAS_041.md)

42. ### [GAS 042 修正火球角度,添加复制,按下shift时普攻](./DetailContent/GAS_042.md)

43. ### [GAS 043 使用MotionWarping插件,进行角色FaceTo功能](./DetailContent/GAS_043.md)

44. ### [GAS 044 当火球发生撞击时产生音效和Niagara粒子,火球飞行时加loop音效绑定到root,持有该音频组件,撞击后停止音效](./DetailContent/GAS_044.md)

45. ### [GAS 045 C++中创建和使用自定义碰撞类型](./DetailContent/GAS_045.md)

46. ### [GAS 046 为火球添加GE:敌人设置和初始化AttributeSet:处理碰撞bug](./DetailContent/GAS_046.md)


___________________________________________________________________________________________

# 操作相关：关键点梳理

___________________________________________________________________________________________

##### 处理关键点
###### 1. 再C++中使用FName插槽名，将武器SK，绑定到角色SK上
###### 2. 使用动画蓝图模板
1. ### [GAS 001 配置项目/设置Mesh/插槽/动画(创建和使用ABP模板)](./DetailContent/GAS_001.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. PlayerController配置鼠标相关设置
###### 2. PlayerController配置增强输入
###### 3. 增强输入配置
###### 4. 增强输入移动形参类型
###### 5. PlayerController的角色移动旋转计算
###### 6. 转身速率配置
###### 7. PlayerControllerRotation映射SpringArm旋转配置
2. ### [GAS 002 配置增强输入/GM/玩家移动/转身速率](./DetailContent/GAS_002.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 接口Interface的使用（比如权限和纯虚函数） 
###### 2. PlayerController中使用 获取鼠标的位置发射射线，返回结果 的函数（只识别block）
###### 3. 自定义边缘发光深度材质 生效相关配置（Post Process Volume生效范围/后期处理材质配置）
###### 4. 在项目文件中定义宏并使用
3. ### [GAS 003 通过(接口)实现(描边)效果](./DetailContent/GAS_003.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 角色PS中创建ASC组件,角色通过PS持有ASC组件和AS组件
###### 2. 调用ASC组件的初始化函数进行初始化（不能在构造中初始化！）
###### 3. ASC组件——网络复制 属性同步模式,一共有3种类型:1.Minimal /2.Mixed /3.Full
###### 4. 当PlayerState存在时 同步给所有客户端 的函数 
4. ### [GAS 004 GAS网络同步的 属性同步模式 类型 和 设置](./DetailContent/GAS_004.md)

___________________________________________________________________________________________

##### 处理关键点

###### 1. GetLifetimeReplicatedProps 此函数在U0bject中 开启 属性复制(RepNotify)后 需要重写这个函数!//此函数规定了:1.哪些参数同步 以及 2.同步的条件
###### 2. 根据AttributeSet基类中写好的宏Get/set/lnit 属性；
###### 3. 为每个属性创建属性复制和相关函数；调用同步函数,设置同步参数；DOREPLIFETIME_CONDITION_NOTIFY宏使用（在UnrealNetwork.h中）
4. GAS调试debug命令showdebug abilitysystem
5. overlap委托和回调绑定
6. 使用const_cast把const变量转化为非const变量
5. ### [GAS 005 设置属性；创建一个加血的血瓶](./DetailContent/GAS_005.md)

___________________________________________________________________________________________


6. ### [GAS 006 创建UI](./DetailContent/GAS_006.md)

___________________________________________________________________________________________

##### 处理关键点
######  下面是结构梳理：
###### 1 MVC(Model->四大数据PC/PS/ASC/AS；
###### 2 View->AuraUserWidget；Control->WidgetController)+使用发布更新的架构
###### 3 1角色（这里是角色，也可以是别的）初始化时调用HUD，根据配置的class在堆区实例化OverlayWidgetController，
###### 4 传入数据更新OverlayWidgetController中的数据（只在初始化时，创建包含四大数据的结构体，才给OverlayWidgetController传入指针数据，后续自行持有指针）
7. ### [GAS 007 项目MVC架构](./DetailContent/GAS_007.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 动态单播,在c++中声明,蓝图中绑定回调

```CPP
AbilitySystemComponent_>GetGameplayAttributeValueChangeDelegate(
    AuraAttributeSet_>GetHealthAttribute()).AddUObject(this,&UOverlayWidgetController::HealthChanged);
```

###### 2. ASC组件 调用 获取属性变化委托,传入特定类型属性,且 回调函数形参 必须为const FOnAttributeChangeData类型

```CPP
void HealthChanged(const FOnAttributeChangeData& Data);
```

8. ### [GAS 008 配置多播](./DetailContent/GAS_008.md)

___________________________________________________________________________________________

##### 处理关键点

###### 1. 此函数使用 `UAbilitySystemBlueprintLibrary` 函数库中的API (检查目标是否实现了IAbilitySystemInterface 接口/若未实现 返回nullptr)
```CPP
UAbilitySystemComponent* TargetASC = UAbilitySystemBlueprintLibrary::GetAbilitySystemComponent(TargetActor);
```

###### 2. 道具类使用GE:
   - //步骤一:ASC中的API创建一个 FGameplayEffectcontextHandle（游戏效果上下文句柄）
   - //步骤二:为上下文添加Source
   - //步骤三: ASC中的API创建一个 FGameplayEffectSpecHandle 类型的（GE句柄）
   - //步骤四:ASC中的API使用GE句柄应用GE到Target或Self

3. GE三种类型 一次性/持续（临时）/永久  的配置
4. StackingType堆叠效果（此处是指增益堆叠）
5. 移除 GE 效果（返回时需要记录FActiveGameplayEffectHandle类变量）
6. GE的Stacking(此处是指减益堆叠)
7. 数组中移除单个数据
9. ### [GAS 009 即时生效GE/持续时间内生效的GE(比如增益BUFF)/永久生效的GE/GE中的Stacking(效果堆叠)](./DetailContent/GAS_009.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. `AuraAttributeSet`中重写虚函数`PreAttributeChange`(属性更改前 预处理)限制属性最大最小值
###### 2. 了解属性更改后 **处理虚函数** `PostGameplayEffectExecute`
###### 3. 实参 `Data` ,几乎能拿到所有信息
###### 4. **给GE数值配表**
10. ### [GAS 010 AttributeSet中限制HP/MP最大最小值:创建药水的表格](./DetailContent/GAS_010.md)

___________________________________________________________________________________________


11. ### [GAS 011 什么是GameplayTags？:创建GameplayTags两种方式:给物体添加标签](./DetailContent/GAS_011.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 使用ASC组件基类中,写好的委托 `OnGameplayEffectAppliedDelegateToSelf`（当应用GE到ASC时触发回调）
###### 2. 一次性道具 配置资产标签`AssetTag`,这样可以在触发回调时通过`FGameplayEffectSpec`类的对象拿到`FGameplayTagContainer`（这个相当于水杯,tag相当于水）
###### 3. 使用`GEngine->AddOnScreenDebugMessage`（相当于`PrintString`）发Message到视口
###### 4. 先创建表格结构体（需要继承`FTableRowBase`！！！）在创建模板类,根据传入的表格查找指定行（`FindRow`,这里行命名实用了tag字符串的格式,便于查找）
###### 5. `UPROPERTY(EditDefaultOnly)`宏//在编辑器中显示并允许编辑这些属性的默认值,但不允许在实例级别进行修改。
###### 6. C++中创建Tag标签:`FGameplayTag::RequestGameplayTag(FName("Message"));`并使用API（父类标签包含子类标签前提下） :子类`Tag.MatchesTag`(父类Tag)检查子类标签中是否包含父类标签,若反过来检查则不生效,请注意！！！
12. ### [GAS 012 绑定GE委托,通过收到的的资产标签,广播信息结构体,触发UI中绑定的WidgetController回调,UI中拿到生成MessageUI的信息](./DetailContent/GAS_012.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 重写后处理函数PostGameplayEffectExecute,使用clamp限制
13. ### [GAS 013 拾取道具的小UI:HP和MP的滞后效果](./DetailContent/GAS_013.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 初始化属性的三种方法
14. ### [GAS 014 配表 初始化属性:GE中的Modifiers中的Coefficient（简单属性计算）](./DetailContent/GAS_014.md)

___________________________________________________________________________________________


15. ### [GAS 015 主要属性和次要属性设计](./DetailContent/GAS_015.md)

___________________________________________________________________________________________


16. ### [GAS 016 创建和配置 主要属性和次要属性:初始化次要属性(使用简单公式)](./DetailContent/GAS_016.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 属性同步 配置
###### 2. UE inline宏 `FORCEINLINE`
17. ### [GAS 017 创建接口(查询对象的等级)](./DetailContent/GAS_017.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 自定义属性计算方式需要创建类`GameplayModMagnitudecalculation`
   - //步骤一:需要依赖的属性 要创建`FGameplayEffectAttributecaptureDefinition`类变量 构造中,给变量配置参数
   - //步骤二:重写虚函数`CalculateBaseMagnitude`并调用核心处理API`GetCapturedAttributeMagnitude`为变量赋值,然后通过`FGameplayEffectSpec`拿到角色数据,计算并返回
   - //步骤三:GE中配置自定义计算方式
18. ### [GAS 018 MMC——Modifier Magnitude calculation(自定义属性计算方式);以及如何使用自定义后的值初始化HP/MP属性](./DetailContent/GAS_018.md)

___________________________________________________________________________________________


19. ### [GAS 019 UI属性面板 显示/隐藏:创建通用按钮UI](./DetailContent/GAS_019.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 创建无类型的纯C++类,创建用于管理GameplayTags的结构体FAuraGameplayTags,创建初始化游戏标签函数,私有时声明一个变量,在源文件中定义
###### 2. 单例类的变量使用（static）
###### 3. 创建自己的AssetManager类,提换引擎默认的资产管理器,重写虚函数StartInitialLoading,在加载完毕时,添加自己的逻辑（项目中的Config文件夹下的DefaultEngine.ini文件中查找(找不到就添加)设置自建的类型AuraAssetManager）
20. ### [GAS 020 创建:1.管理游戏标签结构体;2.自己的资产管理器类;3.创建DataAsset资产:4.制作WidgetController](./DetailContent/GAS_020.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. `UFUNCTION(BlueprintPure,Category="AuraAbilitySystemLibrary|WidgetController",meta=(WorldContext="WorldContextObject"))`
###### 2. 若形参中 有const UObject* WorldContextObject这个作为世界上下文,上面的宏UFUNCTION(meta=(WorldContext="WorldContextObject")),可以自动识别函数的世界上下文
###### 3. 拿数据:PS从PC拿,ASC和AS从PS拿（因为在PS中创建）
21. ### [GAS 021 创建蓝图函数库](./DetailContent/GAS_021.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 模板函数的使用
###### 2. if constexpr 是一种条件编译语句,它允许在编译时进行条件检查,并且只有满足条件的分支代码会被编译。这与普通的 if 语句不同,普通的 if 语句是在运行时进行条件检查。示例:
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
22. ### [GAS 022 创建模板函数——抽象  UAuraAbilitySystemLibrary 里面获取WidgetController的部分](./DetailContent/GAS_022.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 属性菜单发送多播,单独属性的ItemWidgetUI接收,验证tag一致后更新自身信息（使用MachesTag验证）
###### 2. 使用TMap把类型变量与静态函数的函数指针进行绑定
###### 
###### 3. 函数指针格式`返回值类型（*指针名称）（参数类型）`
###### 4. 函数指针使用时格式:`函数指针名();`即可调用
###### 5. 通过ASC组件获取 当属性变化时广播的委托变量/绑定Lambda回调
23. ### [GAS 023 重点！！！(委托绑定/变参函数模板)属性面板UI中绑定委托更新消息](./DetailContent/GAS_023.md)

___________________________________________________________________________________________


24. ### [GAS 024 概念和联网 GA(GameplayAbilities)](./DetailContent/GAS_024.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 只有服务器才能赋予技能
###### 2. 学习技能时,先使用GA的Class创建FGameplayabilitySpec技能规范,然后调用API:`GiveAbilityAndActivateOnce`(这里传入技能规范)才能学习
25. ### [GAS 025 授予能力GA](./DetailContent/GAS_025.md)

___________________________________________________________________________________________


26. ### [GAS 026 GameplayAbility中的Tag——技能互斥](./DetailContent/GAS_026.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 使用C++模板,创建了一个函数模板
###### 2. 具体参考《C++模板》(书我的在微信收藏里)
27. ### [GAS 027 使用数据资产将 输入 与 输入触发的Tag 绑定](./DetailContent/GAS_027.md)

___________________________________________________________________________________________


28. ### [GAS 028 创建自建增强输入组件,创建函数模板](./DetailContent/GAS_028.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 引擎中配置增强输入:`项目设置`->`输入`->`默认输入组件类`
29. ### [GAS 029 AAuraPlayerController中为自建增强输入组件创建并绑定按键回调,引擎中配置增强输入](./DetailContent/GAS_029.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 赋予角色技能时,给 技能GA 添加 动态标签DynamicAbilityTag
###### 2. 调用 ASC组件中的API: GetActivatableAbilities()可以拿到所以可以激活的GA的Spec
###### 3. GA的Spec 中 有一个动态技能标签 DynamicAbilityTags 若技能激活时 会拥有该 Tag
###### 4. 调用 ASC组件中的API: `AbilitySpecInputPressed(AbilitySpec);`会 标记技能的输入状态为已按下
###### 5. 使用 ASC组件中的API: `TryActivateAbility(AbilitySpec.Handle);`尝试激活该技能 若激活技能 会把 `AbilitySpec` 标记为已激活 `IsActive`
###### 6. 使用`AbilitySpec.Handle` 激活该技能`TryActivateAbility(AbilitySpec.Handle);`
30. ### [GAS 030 GA中配置Tag,并在按下和松开按键时的回调函数中设置,保证释放GA时,触发并持有该Tag](./DetailContent/GAS_030.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 了解官方俯视角游戏DS/LS框架下的问题
###### 2. 梳理点击移动的逻辑
31. ### [GAS 031 PC实现点击移动_参考官方 俯视角游戏模板](./DetailContent/GAS_031.md)

___________________________________________________________________________________________


32. ### [GAS 032 PC短按 实现自动移动](./DetailContent/GAS_032.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 样条线API
###### 2. 获取NaviMesh的导航路径NaviPath上的点
33. ### [GAS 033 人物沿样条线运动 获取NaviMesh的Path导航路径上的点](./DetailContent/GAS_033.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 优化逻辑步骤
   - 检查有无重复获取的结果,保存变量,节约运行时开销
   - 检查冗余代码,精简,抽象 逻辑
   - 考虑可能出现的情况和bug,  检查优化逻辑,并修复,参考《防御式编程》
   - 没问题后 去掉Debug和调试
###### 2. C++中的RPC
34. ### [GAS 034 优化PC中的逻辑 运行时勿重复获取结果 精简代码 考虑可能出现的bug](./DetailContent/GAS_034.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. C++构造中设置碰撞通道和类型
###### 2. C++构造中设置抛射物组件参数
35. ### [GAS 035 创建抛射物类,蓝图继承并配置NS,替换地板](./DetailContent/GAS_035.md)

___________________________________________________________________________________________

36. ### [GAS 036 创建新的C++类继承自UAuraGameplayAbility重写ActivateAbility虚函数打印测试](./DetailContent/GAS_036.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 只有服务器才能生成火球:
###### 2. GA中,使用API:`GetAvatarActorFromActorInfo` 拿到使用`该GA的Actor`
###### 3. GA中,使用API:`GetOwningActorFromActorInfo` 获取`Owner`
###### 4. 使用 `GetWorld()->SpawnActorDeferred` `延时生成Actor`(延时生成还需要调用 `FinishSpawning` )
###### 5. GA中通过`WaitGamePlayEvent`,接收事件的Tag,发送时使用`SendGameplayEventToActor`,发送事件Tag
37. ### [GAS 037 GA中在服务器端生成火球](./DetailContent/GAS_037.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. UFUNCTION宏的一些用法

  - `UFUNCTION( meta = ( DisplayName = "TargetDataUnderMouse" ))`             设置在蓝图编辑器中显示的函数名称

  - `UFUNCTION( meta = ( Tooltip = "This is my custom function tooltip" ))`   在蓝图编辑器中显示的提示信息,当鼠标悬停在函数或属性上时显示。

  - `UFUNCTION( meta = ( HidePin="OwningAbility" ))`                          隐藏特定的输入引脚（Pin）

  - `UFUNCTION( meta = ( DefaultToSelf="OwningAbility" )) `                   设置默认值。如果某个引脚没有被连接,蓝图将其值设置 为 self

  - `UFUNCTION( meta = ( BlueprintInternalUseOnly = "true" ))`                蓝图中仅限内部使用 宏

  - `UFUNCTION( meta = ( DevelopmentOnly ))`                                  仅在开发版本中可见,发布版本中隐藏。

###### 2. `UAbilityTask`
  - 在蓝图中调用 `UAbilityTask` 的方法会被视为异步的,这是因为 `UAbilityTask` 类的设计本身就是为了处理`异步任务`。虽然在 C++ 代码中执行逻辑可能是同步的,但 `UAbilityTask` 的机制允许在蓝图中以异步方式使用它们。
38. ### [GAS 038 使用自定义AbilityTasks](./DetailContent/GAS_038.md)

___________________________________________________________________________________________


39. ### [GAS 039 Ability Task中的TargetData处理时间差异的方法流程思路](./DetailContent/GAS_039.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 梳理清楚GAS的`AbilityTask`中`TargetData`的网络同步,时间差异思路梳理:
   - 有两个通信事件:1是`ClientActive`到`ServerActive`:1完成后Server绑定委托到目标集:2是Client的`TargetData`到Server的`TargetData`
   - 若时间顺序为12则没有问题,此时只需要在执行2时检查是否绑定到目标集若绑定说明顺序为12,否则顺序为21
###### 2. 通信需要发送 `FGameplayAbilityTargetDataHandle` 类型数据,如果需要区分数据类型,需要使用从`TargetData`派生的类,赋值并添加到`TargetDataHandle`中
###### 3. GAS预测,看文档吧,太复杂
   - 创建一个 作用域预测窗口
###### 4. 服务器接收时回调参数需要为 `const FGameplayAbilityTargetDataHandle& DataHandle, FGameplayTag ActivationTag`
###### 5. 服务器接收流程:
   - //1.先获取委托并绑定回调 ,使用API:`AbilitySystemComponent.Get()-> AbilityTargetDataSetDelegate`获取委托
   - //2.检查目标数据委托是否已绑定 ,使用API:`AbilitySystemComponent-> CallReplicatedTargetDataDelegatesIfSet` 返回bool:如果未绑定,使用API: `SetWaitingOnRemotePlayerData` 设置等待远程玩家数据
   - //3.回调中 ,执行到这里说明已收到TargetData数据,使用API:`AbilitySystemComponent-> ConsumeClientReplicatedTargetData` 消耗客户端发送的目标数据 `TargetData`(和UI中消耗 鼠标点击 类似):此时检查 若已绑定多播,广播`DataHandle`
40. ### [GAS 040 gas中的预测,Ability Task中,Client端发送 鼠标点击数据的TargetData,并在Server端接收](./DetailContent/GAS_040.md)

___________________________________________________________________________________________


41. ### [GAS 041 预测和预测密钥Predictionkey梳理](./DetailContent/GAS_041.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 使用: `向量.Rotation();` 获取角度FRotator
###### 2. 使用: `角度.Quaternion();` 获取该角度的四元数
###### 3. C++中设置 碰撞通道
###### 4. DS / LS网络复制相关
42. ### [GAS 042 修正火球角度,添加复制,按下shift时普攻](./DetailContent/GAS_042.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. MotionWarping插件使用流程
   - //1.开启插件
   - //2.角色上添加组件
   - //3.检查动画是否为根动画
   - //4.动画蒙太奇中添加MotionWarping通知状态,并配置相关设置
   - //5.在使用时,使用组件->AddOrUpdateWarpTargetFromLocation函数传入要转向的位置(插件内自动计算角度并根据动画状态时长设置旋转速率)
43. ### [GAS 043 使用MotionWarping插件,进行角色FaceTo功能](./DetailContent/GAS_043.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 生成音频调用API: `UGameplayStatics::PlaySoundAtLocation;`生成音频绑定在目标身上API: `UGameplayStatics::SpawnSoundAttached` 此函数返回一个组件,可以使用 `.Stop();` 停止播放
###### 2. 使用Niagara粒子系统需要引模块`Niagara`
###### 3. 生成Niagara粒子调用API: `UNiagaraFunctionLibrary::SpawnSystemAtLocation;`
###### 4. 重写`Destoryed`虚函数时,注意!!!要在`调用父函数之前`写逻辑!
44. ### [GAS 044 当火球发生撞击时产生音效和Niagara粒子,火球飞行时加loop音效绑定到root,持有该音频组件,撞击后停止音效](./DetailContent/GAS_044.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 物体若要碰撞检测需要开启`Generate Overlap Events`
###### 2. 当我们第一次创建自定义碰撞通道时,它会占用游戏追踪1"`ECC_GameTraceChannel1`"这个通道
45. ### [GAS 045 C++中创建和使用自定义碰撞类型](./DetailContent/GAS_045.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 火球携带的不是GE而是`FGameplayEffectSpecHandle`,方便直接使用
###### 2. 重温`初始化AttributeSet`的流程
46. ### [GAS 046 为火球添加GE:敌人设置和初始化AttributeSet:处理碰撞bug](./DetailContent/GAS_046.md)

___________________________________________________________________________________________



















