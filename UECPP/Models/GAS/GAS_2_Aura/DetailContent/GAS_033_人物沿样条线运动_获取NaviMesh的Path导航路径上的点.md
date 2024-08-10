___________________________________________________________________________________________

###### [Go主菜单](../MainMenu.md)
___________________________________________________________________________________________

# GAS_033_人物沿样条线运动_获取NaviMesh的Path导航路径上的点
___________________________________________________________________________________________
## 处理关键点
1. 样条线API
2. 获取NaviMesh的导航路径NaviPath上的点
___________________________________________________________________________________________


# 目录
- [GAS 033 人物沿样条线运动 获取NaviMesh的Path导航路径上的点](#gas-033-人物沿样条线运动-获取navimesh的path导航路径上的点)
  - [处理关键点](#处理关键点)
- [目录](#目录)
    - [视频链接](#视频链接)
    - [创建AutoRun函数](#创建autorun函数)
    - [此时在客户端上有bug无法实现点击移动,且 没有DebugSphere出现,原因是NaviMesh导航没有在客户端上开启。开启步骤:](#此时在客户端上有bug无法实现点击移动且-没有debugsphere出现原因是navimesh导航没有在客户端上开启开启步骤)
    - [此时有bug为,若点击无法到达的地点(比如障碍物正中心)会导致`bAutoRunning`变量无法设置为false。处理方法:](#此时有bug为若点击无法到达的地点比如障碍物正中心会导致bautorunning变量无法设置为false处理方法)
    - [完成,此时效果gif,人物会移动到最后一个NaviMesh点](#完成此时效果gif人物会移动到最后一个navimesh点)


___________________________________________________________________________________________


### 视频链接

  - 【【AI中字】虚幻5C++教程使用GAS制作RPG游戏（一）-哔哩哔哩】 https://b23.tv/Wl5H4dP

___________________________________________________________________________________________


### 创建AutoRun函数

只有bAutoRunninn=true才能进入:先拿到角色:调用样条线API:FindLocationClosestToWorldLocation传入位置返回最近的样条线上的点:调用样条线API:FindDirectionClosestToWorldLocation传入上面获取的样条线上的点;调用角色API:AddMovementInput传入Dir;创建float =  样条线上最近的点与角色要到达的地方的距离;判断,若距离小于最小距离的阈值,设置 bAutoRunning = false

![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_033/01.png?raw=true)

___________________________________________________________________________________________


### 此时在客户端上有bug无法实现点击移动,且 没有DebugSphere出现,原因是NaviMesh导航没有在客户端上开启。开启步骤:

  - GIF

    - GIF:客户端`bAutoRunning = true`表现 
![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_033/02.gif?raw=true)

    - GIF:服务器`bAutoRunning = true`表现 
![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_033/03.gif?raw=true)

  - NaviMesh导航配置,在客户端上开启

    - 英文版 配置 
![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_033/04.jpg?raw=true)

    - 中文版 配置 
![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_033/05.png?raw=true)

___________________________________________________________________________________________


### 此时有bug为,若点击无法到达的地点(比如障碍物正中心)会导致`bAutoRunning`变量无法设置为false。处理方法:

  - 第一步  因为点击是根据碰撞通道ECC_Visibility所以把障碍物的Visibility通道设为忽略
    -  
    ![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_033/06.png?raw=true)

  - 第一步修复完后,还没有解决,因为目标地点还没有修改

  - 第二步 AbilityInputTagReleased函数中,处理要到达的地点:在之前计算获取目标地点时,使用的是被击中的地点作为终点,需要修改为,通过NaviPath路径获取最后一个点,并把这个点的位置给 要到达的地点CachedDestination
    -  
    ![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_033/07.png?raw=true)

___________________________________________________________________________________________


### 完成,此时效果gif,人物会移动到最后一个NaviMesh点 
![图片](https://github.com/liyunlong618/LiYunLongKnowledgeLibrary/blob/main/UECPP/Models/GAS/GAS_2_Aura/DetailContent/Image/GAS_033/08.gif?raw=true)

___________________________________________________________________________________________

[返回最上面](#Go主菜单)
___________________________________________________________________________________________