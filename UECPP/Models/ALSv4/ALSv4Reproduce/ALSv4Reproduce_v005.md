
------

#### [返回菜单](../ALS_Menu.md)

------

# ALSv4复刻v005 创建调试Debug、输入映射、目前的摄像机系统分步骤解释

------

## 目录

[TOC]

------

<details>
<summary>视频链接</summary>

> [高级运动系统解耦和复刻第五期_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ja41197XQ?spm_id_from=333.788.videopod.episodes&vd_source=9e1e64122d802b4f7ab37bd325a89e6c&p=8)

------

</details>

------

## 先创建调试Debug

![image-20250818033211135](./Image/ALSv4Reproduce_v005/image-20250818033211135.png)![BPGraphScreenshot_2025Y-08M-18D-03h-52m-08s-547_00](./Image/ALSv4Reproduce_v005/BPGraphScreenshot_2025Y-08M-18D-03h-52m-08s-547_00.png)

------

## 接下来创建输入映射

我这里使用**增强输入**做了

插件版是有的

1. ALS_Base_CharacterBP中创建两个变量：
   - `float` 类型变量，命名为：`LookUpDownRate` = `1.25f`
   - `float` 类型变量，命名为：`LookLeftRightRate` = `1.25f`
2. 计算一下输入映射和旋转

![image-20250818033450062](./Image/ALSv4Reproduce_v005/image-20250818033450062.png)![image-20250818035331560](./Image/ALSv4Reproduce_v005/image-20250818035331560.png)![BPGraphScreenshot_2025Y-08M-18D-04h-10m-41s-184_00](./Image/ALSv4Reproduce_v005/BPGraphScreenshot_2025Y-08M-18D-04h-10m-41s-184_00.png)

------

## 目前效果gif

![2025-08-18 04-12-54](./Image/ALSv4Reproduce_v005/2025-08-18 04-12-54.gif)

------

## 接下来我将目前所做的摄像机系统分步骤解释一下

### 1.TODO

------

[返回最上面](#返回菜单)

___________________________________________________________________________________________
