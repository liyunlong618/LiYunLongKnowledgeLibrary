


# 思路流程/概念理解

(整理中)

# 操作相关：关键点梳理



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






















