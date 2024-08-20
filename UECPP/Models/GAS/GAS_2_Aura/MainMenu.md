
___________________________________________________________________________________________

# 思路流程/概念理解
___________________________________________________________________________________________

## 目录1

1. ### [**GameplayAbility**](./DetailContent/_GameplayAbility_.md)

2. ### [**GameplayEffect**](./DetailContent/_GameplayEffect_.md)
  - #### [**FGameplayEffectContext** 源码阅读](./DetailContent/_FGameplayEffectContext_.md)

    - [自建**FGameplayEffectContext**(1);了解 网络序列化函数 NetSerialize 的作用](./DetailContent/GAS_067.md)
    - [自建FGameplayEffectContext需要的步骤梳理  UE_5.2和UE_5.3这里的区别](./DetailContent/GAS_068.md)

  - #### [**ExecutionCalculations**(执行计算)](./DetailContent/GAS_061.md)

3. ### [**AbilitySystemComponent**](./DetailContent/_AbilitySystemComponent_.md)

4. ### [**GameplayTag**](./DetailContent/_GameplayTag_.md)

>(整理中)
___________________________________________________________________________________________

# [跳转到 处理关键点](#操作相关关键点梳理)

___________________________________________________________________________________________

## 目录2

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

47. ### [GAS 047 为敌人制作血条UI和MVC](./DetailContent/GAS_047.md)

48. ### [GAS 048 敌人Delay掉血的条](./DetailContent/GAS_048.md)

49. ### [GAS 049 RPG角色分类](./DetailContent/GAS_049.md)

50. ### [GAS 050 创建敌人类型枚举和敌人数据结构体](./DetailContent/GAS_050.md)

51. ### [GAS 051 使用表格创建CSV和Json;导入CSV/Json生成表格](./DetailContent/GAS_051.md)

52. ### [GAS 052 初始化敌人属性](./DetailContent/GAS_052.md)

53. ### [GAS 053 还没编辑完](./DetailContent/GAS_053.md)

54. ### [GAS 054 创建伤害元属性](./DetailContent/GAS_054.md)

55. ### [GAS 055 使用GE的 `Magnitude` 中的 `Set By Caller`  的流程](./DetailContent/GAS_055.md)

56. ### [GAS 056 给GA加伤害配表，并在使用GE时，使用曲线表格中的数据](./DetailContent/GAS_056.md)

57. ### [GAS 057 敌人受击反应](./DetailContent/GAS_057.md)

58. ### [GAS 058 处理敌人死亡效果，C++中开启物理模拟/使用布娃娃](./DetailContent/GAS_058.md)

59. ### [GAS 059 使用敌人的溶解材质，C++设置DynamicMaterial在蓝图中使用Timeline](./DetailContent/GAS_059.md)

60. ### [GAS 060 显示伤害数字UI](./DetailContent/GAS_060.md)

62. ### [GAS 062 使用ExecutionCalculations计算伤害](./DetailContent/GAS_062.md)

63. ### [GAS 063 实现格挡计算；在C++中使用SetByCaller](./DetailContent/GAS_063.md)

64. ### [GAS 064 计算护甲穿透;捕获Source和Target属性；C++中获取曲线表格数据](./DetailContent/GAS_064.md)

65. ### [GAS 065 实现暴击率/暴伤/暴击抗性](./DetailContent/GAS_065.md)


67. ### [GAS 067 自建**FGameplayEffectContext**(1);了解 网络序列化函数 NetSerialize 的作用](./DetailContent/GAS_067.md)

68. ### [GAS 068 自建FGameplayEffectContext(2)；重写 模板结构体TStructOpsTypeTraits；重写 虚函数Duplicate；UE_5.2和UE_5.3这里的区别；自建FGameplayEffectContext需要的步骤梳理](./DetailContent/GAS_068.md)

69. ### [GAS 069 创建自建的全局管理类AbilitySystemGlobles应用自建的FGameplayEffectContext类](./DetailContent/GAS_069.md)

70. ### [GAS 070 现在需要在 ExecCalc_Damage 中设置参数，并在AS的后处理函数中获取 自建 Context 上携带的 bool](./DetailContent/GAS_070.md)

71. ### [GAS 071 创建多种属性伤害类型](./DetailContent/GAS_071.md)

72. ### [GAS 072 属性伤害抗性](./DetailContent/GAS_072.md)

73. ### [GAS 073](./DetailContent/GAS_073.md)

74. ### [GAS 074](./DetailContent/GAS_074.md)

75. ### [GAS 075](./DetailContent/GAS_075.md)

76. ### [GAS 076](./DetailContent/GAS_076.md)

77. ### [GAS 077](./DetailContent/GAS_077.md)

78. ### [GAS 078](./DetailContent/GAS_078.md)

79. ### [GAS 079](./DetailContent/GAS_079.md)

80. ### [GAS 080](./DetailContent/GAS_080.md)

81. ### [GAS 081](./DetailContent/GAS_081.md)

82. ### [GAS 082](./DetailContent/GAS_082.md)

83. ### [GAS 083](./DetailContent/GAS_083.md)

84. ### [GAS 084](./DetailContent/GAS_084.md)

85. ### [GAS 085](./DetailContent/GAS_085.md)

86. ### [GAS 086](./DetailContent/GAS_086.md)

87. ### [GAS 087](./DetailContent/GAS_087.md)

88. ### [GAS 088](./DetailContent/GAS_088.md)

89. ### [GAS 089](./DetailContent/GAS_089.md)

90. ### [GAS 090](./DetailContent/GAS_090.md)

91. ### [GAS 091](./DetailContent/GAS_091.md)

92. ### [GAS 092](./DetailContent/GAS_092.md)

93. ### [GAS 093](./DetailContent/GAS_093.md)

94. ### [GAS 094](./DetailContent/GAS_094.md)

95. ### [GAS 095](./DetailContent/GAS_095.md)

96. ### [GAS 096](./DetailContent/GAS_096.md)

97. ### [GAS 097](./DetailContent/GAS_097.md)

98. ### [GAS 098](./DetailContent/GAS_098.md)

99. ### [GAS 099](./DetailContent/GAS_099.md)

100. ### [GAS 100](./DetailContent/GAS_100.md)

101. ### [GAS 101](./DetailContent/GAS_101.md)

102. ### [GAS 102](./DetailContent/GAS_102.md)

103. ### [GAS 103](./DetailContent/GAS_103.md)

104. ### [GAS 104](./DetailContent/GAS_104.md)

105. ### [GAS 105](./DetailContent/GAS_105.md)

106. ### [GAS 106](./DetailContent/GAS_106.md)

107. ### [GAS 107](./DetailContent/GAS_107.md)

108. ### [GAS 108](./DetailContent/GAS_108.md)

109. ### [GAS 109](./DetailContent/GAS_109.md)

110. ### [GAS 110](./DetailContent/GAS_110.md)

111. ### [GAS 111](./DetailContent/GAS_111.md)

112. ### [GAS 112](./DetailContent/GAS_112.md)

113. ### [GAS 113](./DetailContent/GAS_113.md)

114. ### [GAS 114](./DetailContent/GAS_114.md)

115. ### [GAS 115](./DetailContent/GAS_115.md)

116. ### [GAS 116](./DetailContent/GAS_116.md)

117. ### [GAS 117](./DetailContent/GAS_117.md)

118. ### [GAS 118](./DetailContent/GAS_118.md)

119. ### [GAS 119](./DetailContent/GAS_119.md)

120. ### [GAS 120](./DetailContent/GAS_120.md)

121. ### [GAS 121](./DetailContent/GAS_121.md)

122. ### [GAS 122](./DetailContent/GAS_122.md)

123. ### [GAS 123](./DetailContent/GAS_123.md)

124. ### [GAS 124](./DetailContent/GAS_124.md)

125. ### [GAS 125](./DetailContent/GAS_125.md)

126. ### [GAS 126](./DetailContent/GAS_126.md)

127. ### [GAS 127](./DetailContent/GAS_127.md)

128. ### [GAS 128](./DetailContent/GAS_128.md)

129. ### [GAS 129](./DetailContent/GAS_129.md)

130. ### [GAS 130](./DetailContent/GAS_130.md)

131. ### [GAS 131](./DetailContent/GAS_131.md)

132. ### [GAS 132](./DetailContent/GAS_132.md)

133. ### [GAS 133](./DetailContent/GAS_133.md)

134. ### [GAS 134](./DetailContent/GAS_134.md)

135. ### [GAS 135](./DetailContent/GAS_135.md)

136. ### [GAS 136](./DetailContent/GAS_136.md)

137. ### [GAS 137](./DetailContent/GAS_137.md)

138. ### [GAS 138](./DetailContent/GAS_138.md)

139. ### [GAS 139](./DetailContent/GAS_139.md)

140. ### [GAS 140](./DetailContent/GAS_140.md)

141. ### [GAS 141](./DetailContent/GAS_141.md)

142. ### [GAS 142](./DetailContent/GAS_142.md)

143. ### [GAS 143](./DetailContent/GAS_143.md)

144. ### [GAS 144](./DetailContent/GAS_144.md)

145. ### [GAS 145](./DetailContent/GAS_145.md)

146. ### [GAS 146](./DetailContent/GAS_146.md)

147. ### [GAS 147](./DetailContent/GAS_147.md)

148. ### [GAS 148](./DetailContent/GAS_148.md)

149. ### [GAS 149](./DetailContent/GAS_149.md)

150. ### [GAS 150](./DetailContent/GAS_150.md)

151. ### [GAS 151](./DetailContent/GAS_151.md)

152. ### [GAS 152](./DetailContent/GAS_152.md)

153. ### [GAS 153](./DetailContent/GAS_153.md)

154. ### [GAS 154](./DetailContent/GAS_154.md)

155. ### [GAS 155](./DetailContent/GAS_155.md)

156. ### [GAS 156](./DetailContent/GAS_156.md)

157. ### [GAS 157](./DetailContent/GAS_157.md)

158. ### [GAS 158](./DetailContent/GAS_158.md)

159. ### [GAS 159](./DetailContent/GAS_159.md)

160. ### [GAS 160](./DetailContent/GAS_160.md)

161. ### [GAS 161](./DetailContent/GAS_161.md)

162. ### [GAS 162](./DetailContent/GAS_162.md)

163. ### [GAS 163](./DetailContent/GAS_163.md)

164. ### [GAS 164](./DetailContent/GAS_164.md)

165. ### [GAS 165](./DetailContent/GAS_165.md)

166. ### [GAS 166](./DetailContent/GAS_166.md)

167. ### [GAS 167](./DetailContent/GAS_167.md)

168. ### [GAS 168](./DetailContent/GAS_168.md)

169. ### [GAS 169](./DetailContent/GAS_169.md)

170. ### [GAS 170](./DetailContent/GAS_170.md)

171. ### [GAS 171](./DetailContent/GAS_171.md)

172. ### [GAS 172](./DetailContent/GAS_172.md)

173. ### [GAS 173](./DetailContent/GAS_173.md)

174. ### [GAS 174](./DetailContent/GAS_174.md)

175. ### [GAS 175](./DetailContent/GAS_175.md)

176. ### [GAS 176](./DetailContent/GAS_176.md)

177. ### [GAS 177](./DetailContent/GAS_177.md)

178. ### [GAS 178](./DetailContent/GAS_178.md)

179. ### [GAS 179](./DetailContent/GAS_179.md)

180. ### [GAS 180](./DetailContent/GAS_180.md)

181. ### [GAS 181](./DetailContent/GAS_181.md)

182. ### [GAS 182](./DetailContent/GAS_182.md)

183. ### [GAS 183](./DetailContent/GAS_183.md)

184. ### [GAS 184](./DetailContent/GAS_184.md)

185. ### [GAS 185](./DetailContent/GAS_185.md)

186. ### [GAS 186](./DetailContent/GAS_186.md)

187. ### [GAS 187](./DetailContent/GAS_187.md)

188. ### [GAS 188](./DetailContent/GAS_188.md)

189. ### [GAS 189](./DetailContent/GAS_189.md)

190. ### [GAS 190](./DetailContent/GAS_190.md)

191. ### [GAS 191](./DetailContent/GAS_191.md)

192. ### [GAS 192](./DetailContent/GAS_192.md)

193. ### [GAS 193](./DetailContent/GAS_193.md)

194. ### [GAS 194](./DetailContent/GAS_194.md)

195. ### [GAS 195](./DetailContent/GAS_195.md)

196. ### [GAS 196](./DetailContent/GAS_196.md)

197. ### [GAS 197](./DetailContent/GAS_197.md)

198. ### [GAS 198](./DetailContent/GAS_198.md)

199. ### [GAS 199](./DetailContent/GAS_199.md)

200. ### [GAS 200](./DetailContent/GAS_200.md)


___________________________________________________________________________________________

# 操作相关：关键点梳理

___________________________________________________________________________________________

###### 处理关键点
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
###### 4. GAS调试debug命令showdebug abilitysystem
###### 5. overlap委托和回调绑定
###### 6. 使用const_cast把const变量转化为非const变量

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

##### 处理关键点
###### 1. A类中绑定和广播B类中的动态多播(这里A类和B类是举例说明，非特指)
###### 2. 回顾 **`UObject`** 类都有哪些 **`功能`** 和 **`子类`** ？
###### 3. 当属性值发生变化触发的多播委托如何获取？
###### 4. **使用变量常会涉及到的问题：**
- //1.何时初始化？
- //2.何时绑定委托？
- //3.何时广播？
- //4.何时广播初始值？
47. ### [GAS 047 为敌人制作血条UI和MVC](./DetailContent/GAS_047.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 计时器的逻辑
###### 2. 内部持有状态变量的思路
###### 3. Tick优化(不用的技能记得关闭Tick)

48. ### [GAS 048 敌人Delay掉血的条](./DetailContent/GAS_048.md)

___________________________________________________________________________________________

49. ### [GAS 049 RPG角色分类](./DetailContent/GAS_049.md)

___________________________________________________________________________________________

50. ### [GAS 050 创建敌人类型枚举和敌人数据结构体](./DetailContent/GAS_050.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 使用UE引擎内表格导出CSV和Json
###### 2. 导入CSV和Json
###### 3. 三种曲线表格区别和特点

51. ### [GAS 051 使用表格创建CSV和Json;导入CSV/Json生成表格](./DetailContent/GAS_051.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 蓝图识别的反射宏修改元数据
###### 2. 创建GE并应用到自身的步骤
###### 3. 创建GE并应用到自身最容易忘哪一步？
###### 4. 通过FGameplayEffectSpecHandle对象，都能拿到哪些数据？

52. ### [GAS 052 初始化敌人属性](./DetailContent/GAS_052.md)

___________________________________________________________________________________________

53. ### [GAS 053 还没编辑完](./DetailContent/GAS_053.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 元属性特性
###### 2. 元属性从创建到使用
54. ### [GAS 054 创建伤害元属性](./DetailContent/GAS_054.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 使用GE的 `Magnitude` 中的 `Set By Caller`  的流程

55. ### [GAS 055 使用GE的 `Magnitude` 中的 `Set By Caller`  的流程](./DetailContent/GAS_055.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 可以在蓝图中配表的数据类型 `FScalableFloat` 
###### 2.  `FScalableFloat` 的使用API
###### 3. 在 `GA` 中获取等级


56. ### [GAS 056 给GA加伤害配表，并在使用GE时，使用曲线表格中的数据](./DetailContent/GAS_056.md)

___________________________________________________________________________________________

##### 处理关键点

###### 1. 梳理GA\GE\Tag互相触发的逻辑
###### 2. 监听`身上FGameplayTag的更改`的委托
###### 3. 如何赋予GA和激活
###### 4. 使用Tag触发技能
###### 5. `使用GE的Class触发GE`的函数
###### 6. 给GA配置Tag
###### 7. GA的实例化策略区别

57. ### [GAS 057 敌人受击反应](./DetailContent/GAS_057.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 模拟物理开启步骤

58. ### [GAS 058 处理敌人死亡效果，C++中开启物理模拟/使用布娃娃](./DetailContent/GAS_058.md)


___________________________________________________________________________________________

## 处理关键点
###### 1. 创建动态材质实例C++类型和API

59. ### [GAS 059 使用敌人的溶解材质，C++设置DynamicMaterial在蓝图中使用Timeline](./DetailContent/GAS_059.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 动态生成组件
###### 2. 伤害文字UI动效参考
###### 3. 有时间看下 `FGameplayModifierEvaluatedData` 这个里面都有什么数据?怎么拿?

60. ### [GAS 060 显示伤害数字UI](./DetailContent/GAS_060.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 使用ExecutionCalculations计算伤害需要先 `捕获属性` 再计算并应用  `捕获属性` 
###### 2.  `捕获属性` 的两种：一种自己创建；一种是用官方宏
###### 3.  `捕获属性` 五个步骤
###### 4. 计算并应用  `捕获属性` 五个步骤
###### 5. 回顾自定义计算类MMC的流程

62. ### [GAS 062 使用ExecutionCalculations计算伤害](./DetailContent/GAS_062.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 捕获属性流程
###### 2. 生成处理随机数/概率

63. ### [GAS 063 实现格挡计算；在C++中使用SetByCaller](./DetailContent/GAS_063.md)

___________________________________________________________________________________________

##### 处理关键点
###### 1. 使用官方宏捕获和使用源属性
###### 2. 在ExecutionCalculations中获取使用曲线表格

64. ### [GAS 064 计算护甲穿透;捕获Source和Target属性；C++中获取曲线表格数据](./DetailContent/GAS_064.md)

___________________________________________________________________________________________

65. ### [GAS 065 实现暴击率/暴伤/暴击抗性](./DetailContent/GAS_065.md)

___________________________________________________________________________________________

##### 了解关键点
###### 1. 了解 脚本化结构体 函数 `GetScriptStruct` 
###### 2. 了解 `网络序列化函数`  `NetSerialize` 的作用
###### 3. 了解 `uint8`
###### 4. `FArchive` 结构体 在网络序列化中的作用

67. ### [GAS 067 自建**FGameplayEffectContext**(1);了解 网络序列化函数 NetSerialize 的作用](./DetailContent/GAS_067.md)

___________________________________________________________________________________________

##### 处理关键点

###### 1. 重写 网络序列化函数 `NetSerialize`，使用 `uint32` 无符号整数来 重新记录序列化信息
###### 2. 自建FGameplayEffectContext需要的步骤：
   - ###### 第一步：**继承** `FGameplayEffectContext`
   - ###### 第二步：**重写 `GetScriptStruct`**: 实现该函数以使自定义结构在反射系统中被正确识别和处理。 `(UE_5.3有变更)`
   - ###### 第三步：**重写 `NetSerialize`**: 定义如何在网络传输时序列化和反序列化自定义数据。
   - ###### 第四步：**重写 `Duplicate`**: 确保自定义上下文能够被深拷贝以支持复杂数据的复制。 `(UE_5.3有变更)`
   - ###### 第五步：**重写 `TStructOpsTypeTraits`**: 设置结构体的操作特性，以控制其复制、序列化和比较行为。 `(UE_5.3有变更)

68. ### [GAS 068 自建FGameplayEffectContext(2)；重写 模板结构体TStructOpsTypeTraits；重写 虚函数Duplicate；UE_5.2和UE_5.3这里的区别；自建FGameplayEffectContext需要的步骤梳理](./DetailContent/GAS_068.md)

___________________________________________________________________________________________

##### 处理关键点

###### 1. 应用 `FGameplayEffectContext` 的步骤

###### 2. 应用自建的 `AbilitySystemGlobles`的步骤

   - ###### 创建 `AbilitySystemGlobles` c++类

   - ###### `DefaultGame.ini` 中配置

69. ### [GAS 069 创建自建的全局管理类AbilitySystemGlobles应用自建的FGameplayEffectContext类](./DetailContent/GAS_069.md)

___________________________________________________________________________________________

##### 处理关键点

###### 1. 如何把拿到的 `FGameplayEffectContext` 类型转换成自己的 `FAuraGameplayEffectContext`
###### 2. 结构梳理：
   - ###### 谁送 —— 在 `ExecCalc_Damage` 中设置参数
   - ###### 谁拿 —— 在 `AS` 的后处理函数中获取 自建 `Context` 上携带的 `bool`
   - ###### 怎么拿 —— 通过蓝图函数库 `AuraAbilitySystemLibrary` 创建 `Set` / `Get` 函数

70. ### [GAS 070 现在需要在 ExecCalc_Damage 中设置参数，并在AS的后处理函数中获取 自建 Context 上携带的 bool](./DetailContent/GAS_070.md)

___________________________________________________________________________________________

71. ### [GAS 071 创建多种属性伤害类型](./DetailContent/GAS_071.md)

___________________________________________________________________________________________

72. ### [GAS 072 属性伤害抗性](./DetailContent/GAS_072.md)

___________________________________________________________________________________________

##### 处理关键点

73. ### [GAS 073](./DetailContent/GAS_073.md)

___________________________________________________________________________________________

##### 处理关键点

74. ### [GAS 074](./DetailContent/GAS_074.md)

___________________________________________________________________________________________

##### 处理关键点

75. ### [GAS 075](./DetailContent/GAS_075.md)

___________________________________________________________________________________________

##### 处理关键点

76. ### [GAS 076](./DetailContent/GAS_076.md)

___________________________________________________________________________________________

##### 处理关键点

77. ### [GAS 077](./DetailContent/GAS_077.md)

___________________________________________________________________________________________

##### 处理关键点

78. ### [GAS 078](./DetailContent/GAS_078.md)

___________________________________________________________________________________________

##### 处理关键点

79. ### [GAS 079](./DetailContent/GAS_079.md)

___________________________________________________________________________________________

##### 处理关键点

80. ### [GAS 080](./DetailContent/GAS_080.md)

___________________________________________________________________________________________

##### 处理关键点

81. ### [GAS 081](./DetailContent/GAS_081.md)

___________________________________________________________________________________________

##### 处理关键点

82. ### [GAS 082](./DetailContent/GAS_082.md)

___________________________________________________________________________________________

##### 处理关键点

83. ### [GAS 083](./DetailContent/GAS_083.md)

___________________________________________________________________________________________

##### 处理关键点

84. ### [GAS 084](./DetailContent/GAS_084.md)

___________________________________________________________________________________________

##### 处理关键点

85. ### [GAS 085](./DetailContent/GAS_085.md)

___________________________________________________________________________________________

##### 处理关键点

86. ### [GAS 086](./DetailContent/GAS_086.md)

___________________________________________________________________________________________

##### 处理关键点

87. ### [GAS 087](./DetailContent/GAS_087.md)

___________________________________________________________________________________________

##### 处理关键点

88. ### [GAS 088](./DetailContent/GAS_088.md)

___________________________________________________________________________________________

##### 处理关键点

89. ### [GAS 089](./DetailContent/GAS_089.md)

___________________________________________________________________________________________

##### 处理关键点

90. ### [GAS 090](./DetailContent/GAS_090.md)

___________________________________________________________________________________________

##### 处理关键点

91. ### [GAS 091](./DetailContent/GAS_091.md)

___________________________________________________________________________________________

##### 处理关键点

92. ### [GAS 092](./DetailContent/GAS_092.md)

___________________________________________________________________________________________

##### 处理关键点

93. ### [GAS 093](./DetailContent/GAS_093.md)

___________________________________________________________________________________________

##### 处理关键点

94. ### [GAS 094](./DetailContent/GAS_094.md)

___________________________________________________________________________________________

##### 处理关键点

95. ### [GAS 095](./DetailContent/GAS_095.md)

___________________________________________________________________________________________

##### 处理关键点

96. ### [GAS 096](./DetailContent/GAS_096.md)

___________________________________________________________________________________________

##### 处理关键点

97. ### [GAS 097](./DetailContent/GAS_097.md)

___________________________________________________________________________________________

##### 处理关键点

98. ### [GAS 098](./DetailContent/GAS_098.md)

___________________________________________________________________________________________

##### 处理关键点

99. ### [GAS 099](./DetailContent/GAS_099.md)

___________________________________________________________________________________________

##### 处理关键点

100. ### [GAS 100](./DetailContent/GAS_100.md)

___________________________________________________________________________________________

##### 处理关键点

101. ### [GAS 101](./DetailContent/GAS_101.md)

___________________________________________________________________________________________

##### 处理关键点

102. ### [GAS 102](./DetailContent/GAS_102.md)

___________________________________________________________________________________________

##### 处理关键点

103. ### [GAS 103](./DetailContent/GAS_103.md)

___________________________________________________________________________________________

##### 处理关键点

104. ### [GAS 104](./DetailContent/GAS_104.md)

___________________________________________________________________________________________

##### 处理关键点

105. ### [GAS 105](./DetailContent/GAS_105.md)

___________________________________________________________________________________________

##### 处理关键点

106. ### [GAS 106](./DetailContent/GAS_106.md)

___________________________________________________________________________________________

##### 处理关键点

107. ### [GAS 107](./DetailContent/GAS_107.md)

___________________________________________________________________________________________

##### 处理关键点

108. ### [GAS 108](./DetailContent/GAS_108.md)

___________________________________________________________________________________________

##### 处理关键点

109. ### [GAS 109](./DetailContent/GAS_109.md)

___________________________________________________________________________________________

##### 处理关键点

110. ### [GAS 110](./DetailContent/GAS_110.md)

___________________________________________________________________________________________

##### 处理关键点

111. ### [GAS 111](./DetailContent/GAS_111.md)

___________________________________________________________________________________________

##### 处理关键点

112. ### [GAS 112](./DetailContent/GAS_112.md)

___________________________________________________________________________________________

##### 处理关键点

113. ### [GAS 113](./DetailContent/GAS_113.md)

___________________________________________________________________________________________

##### 处理关键点

114. ### [GAS 114](./DetailContent/GAS_114.md)

___________________________________________________________________________________________

##### 处理关键点

115. ### [GAS 115](./DetailContent/GAS_115.md)

___________________________________________________________________________________________

##### 处理关键点

116. ### [GAS 116](./DetailContent/GAS_116.md)

___________________________________________________________________________________________

##### 处理关键点

117. ### [GAS 117](./DetailContent/GAS_117.md)

___________________________________________________________________________________________

##### 处理关键点

118. ### [GAS 118](./DetailContent/GAS_118.md)

___________________________________________________________________________________________

##### 处理关键点

119. ### [GAS 119](./DetailContent/GAS_119.md)

___________________________________________________________________________________________

##### 处理关键点

120. ### [GAS 120](./DetailContent/GAS_120.md)

___________________________________________________________________________________________

##### 处理关键点

121. ### [GAS 121](./DetailContent/GAS_121.md)

___________________________________________________________________________________________

##### 处理关键点

122. ### [GAS 122](./DetailContent/GAS_122.md)

___________________________________________________________________________________________

##### 处理关键点

123. ### [GAS 123](./DetailContent/GAS_123.md)

___________________________________________________________________________________________

##### 处理关键点

124. ### [GAS 124](./DetailContent/GAS_124.md)

___________________________________________________________________________________________

##### 处理关键点

125. ### [GAS 125](./DetailContent/GAS_125.md)

___________________________________________________________________________________________

##### 处理关键点

126. ### [GAS 126](./DetailContent/GAS_126.md)

___________________________________________________________________________________________

##### 处理关键点

127. ### [GAS 127](./DetailContent/GAS_127.md)

___________________________________________________________________________________________

##### 处理关键点

128. ### [GAS 128](./DetailContent/GAS_128.md)

___________________________________________________________________________________________

##### 处理关键点

129. ### [GAS 129](./DetailContent/GAS_129.md)

___________________________________________________________________________________________

##### 处理关键点

130. ### [GAS 130](./DetailContent/GAS_130.md)

___________________________________________________________________________________________

##### 处理关键点

131. ### [GAS 131](./DetailContent/GAS_131.md)

___________________________________________________________________________________________

##### 处理关键点

132. ### [GAS 132](./DetailContent/GAS_132.md)

___________________________________________________________________________________________

##### 处理关键点

133. ### [GAS 133](./DetailContent/GAS_133.md)

___________________________________________________________________________________________

##### 处理关键点

134. ### [GAS 134](./DetailContent/GAS_134.md)

___________________________________________________________________________________________

##### 处理关键点

135. ### [GAS 135](./DetailContent/GAS_135.md)

___________________________________________________________________________________________

##### 处理关键点

136. ### [GAS 136](./DetailContent/GAS_136.md)

___________________________________________________________________________________________

##### 处理关键点

137. ### [GAS 137](./DetailContent/GAS_137.md)

___________________________________________________________________________________________

##### 处理关键点

138. ### [GAS 138](./DetailContent/GAS_138.md)

___________________________________________________________________________________________

##### 处理关键点

139. ### [GAS 139](./DetailContent/GAS_139.md)

___________________________________________________________________________________________

##### 处理关键点

140. ### [GAS 140](./DetailContent/GAS_140.md)

___________________________________________________________________________________________

##### 处理关键点

141. ### [GAS 141](./DetailContent/GAS_141.md)

___________________________________________________________________________________________

##### 处理关键点

142. ### [GAS 142](./DetailContent/GAS_142.md)

___________________________________________________________________________________________

##### 处理关键点

143. ### [GAS 143](./DetailContent/GAS_143.md)

___________________________________________________________________________________________

##### 处理关键点

144. ### [GAS 144](./DetailContent/GAS_144.md)

___________________________________________________________________________________________

##### 处理关键点

145. ### [GAS 145](./DetailContent/GAS_145.md)

___________________________________________________________________________________________

##### 处理关键点

146. ### [GAS 146](./DetailContent/GAS_146.md)

___________________________________________________________________________________________

##### 处理关键点

147. ### [GAS 147](./DetailContent/GAS_147.md)

___________________________________________________________________________________________

##### 处理关键点

148. ### [GAS 148](./DetailContent/GAS_148.md)

___________________________________________________________________________________________

##### 处理关键点

149. ### [GAS 149](./DetailContent/GAS_149.md)

___________________________________________________________________________________________

##### 处理关键点

150. ### [GAS 150](./DetailContent/GAS_150.md)

___________________________________________________________________________________________

##### 处理关键点

151. ### [GAS 151](./DetailContent/GAS_151.md)

___________________________________________________________________________________________

##### 处理关键点

152. ### [GAS 152](./DetailContent/GAS_152.md)

___________________________________________________________________________________________

##### 处理关键点

153. ### [GAS 153](./DetailContent/GAS_153.md)

___________________________________________________________________________________________

##### 处理关键点

154. ### [GAS 154](./DetailContent/GAS_154.md)

___________________________________________________________________________________________

##### 处理关键点

155. ### [GAS 155](./DetailContent/GAS_155.md)

___________________________________________________________________________________________

##### 处理关键点

156. ### [GAS 156](./DetailContent/GAS_156.md)

___________________________________________________________________________________________

##### 处理关键点

157. ### [GAS 157](./DetailContent/GAS_157.md)

___________________________________________________________________________________________

##### 处理关键点

158. ### [GAS 158](./DetailContent/GAS_158.md)

___________________________________________________________________________________________

##### 处理关键点

159. ### [GAS 159](./DetailContent/GAS_159.md)

___________________________________________________________________________________________

##### 处理关键点

160. ### [GAS 160](./DetailContent/GAS_160.md)

___________________________________________________________________________________________

##### 处理关键点

161. ### [GAS 161](./DetailContent/GAS_161.md)

___________________________________________________________________________________________

##### 处理关键点

162. ### [GAS 162](./DetailContent/GAS_162.md)

___________________________________________________________________________________________

##### 处理关键点

163. ### [GAS 163](./DetailContent/GAS_163.md)

___________________________________________________________________________________________

##### 处理关键点

164. ### [GAS 164](./DetailContent/GAS_164.md)

___________________________________________________________________________________________

##### 处理关键点

165. ### [GAS 165](./DetailContent/GAS_165.md)

___________________________________________________________________________________________

##### 处理关键点

166. ### [GAS 166](./DetailContent/GAS_166.md)

___________________________________________________________________________________________

##### 处理关键点

167. ### [GAS 167](./DetailContent/GAS_167.md)

___________________________________________________________________________________________

##### 处理关键点

168. ### [GAS 168](./DetailContent/GAS_168.md)

___________________________________________________________________________________________

##### 处理关键点

169. ### [GAS 169](./DetailContent/GAS_169.md)

___________________________________________________________________________________________

##### 处理关键点

170. ### [GAS 170](./DetailContent/GAS_170.md)

___________________________________________________________________________________________

##### 处理关键点

171. ### [GAS 171](./DetailContent/GAS_171.md)

___________________________________________________________________________________________

##### 处理关键点

172. ### [GAS 172](./DetailContent/GAS_172.md)

___________________________________________________________________________________________

##### 处理关键点

173. ### [GAS 173](./DetailContent/GAS_173.md)

___________________________________________________________________________________________

##### 处理关键点

174. ### [GAS 174](./DetailContent/GAS_174.md)

___________________________________________________________________________________________

##### 处理关键点

175. ### [GAS 175](./DetailContent/GAS_175.md)

___________________________________________________________________________________________

##### 处理关键点

176. ### [GAS 176](./DetailContent/GAS_176.md)

___________________________________________________________________________________________

##### 处理关键点

177. ### [GAS 177](./DetailContent/GAS_177.md)

___________________________________________________________________________________________

##### 处理关键点

178. ### [GAS 178](./DetailContent/GAS_178.md)

___________________________________________________________________________________________

##### 处理关键点

179. ### [GAS 179](./DetailContent/GAS_179.md)

___________________________________________________________________________________________

##### 处理关键点

180. ### [GAS 180](./DetailContent/GAS_180.md)

___________________________________________________________________________________________

##### 处理关键点

181. ### [GAS 181](./DetailContent/GAS_181.md)

___________________________________________________________________________________________

##### 处理关键点

182. ### [GAS 182](./DetailContent/GAS_182.md)

___________________________________________________________________________________________

##### 处理关键点

183. ### [GAS 183](./DetailContent/GAS_183.md)

___________________________________________________________________________________________

##### 处理关键点

184. ### [GAS 184](./DetailContent/GAS_184.md)

___________________________________________________________________________________________

##### 处理关键点

185. ### [GAS 185](./DetailContent/GAS_185.md)

___________________________________________________________________________________________

##### 处理关键点

186. ### [GAS 186](./DetailContent/GAS_186.md)

___________________________________________________________________________________________

##### 处理关键点

187. ### [GAS 187](./DetailContent/GAS_187.md)

___________________________________________________________________________________________

##### 处理关键点

188. ### [GAS 188](./DetailContent/GAS_188.md)

___________________________________________________________________________________________

##### 处理关键点

189. ### [GAS 189](./DetailContent/GAS_189.md)

___________________________________________________________________________________________

##### 处理关键点

190. ### [GAS 190](./DetailContent/GAS_190.md)

___________________________________________________________________________________________

##### 处理关键点

191. ### [GAS 191](./DetailContent/GAS_191.md)

___________________________________________________________________________________________

##### 处理关键点

192. ### [GAS 192](./DetailContent/GAS_192.md)

___________________________________________________________________________________________

##### 处理关键点

193. ### [GAS 193](./DetailContent/GAS_193.md)

___________________________________________________________________________________________

##### 处理关键点

194. ### [GAS 194](./DetailContent/GAS_194.md)

___________________________________________________________________________________________

##### 处理关键点

195. ### [GAS 195](./DetailContent/GAS_195.md)

___________________________________________________________________________________________

##### 处理关键点

196. ### [GAS 196](./DetailContent/GAS_196.md)

___________________________________________________________________________________________

##### 处理关键点

197. ### [GAS 197](./DetailContent/GAS_197.md)

___________________________________________________________________________________________

##### 处理关键点

198. ### [GAS 198](./DetailContent/GAS_198.md)

___________________________________________________________________________________________

##### 处理关键点

199. ### [GAS 199](./DetailContent/GAS_199.md)

___________________________________________________________________________________________

##### 处理关键点

200. ### [GAS 200](./DetailContent/GAS_200.md)

___________________________________________________________________________________________
