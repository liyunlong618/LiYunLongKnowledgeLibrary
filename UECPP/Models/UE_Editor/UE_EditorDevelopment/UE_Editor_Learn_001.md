___________________________________________________________________________________________
###### [GoMenu](../UE_EditorMenu.md)
___________________________________________________________________________________________
# 001 创建插件和引入模块
___________________________________________________________________________________________


## 目录

[TOC]

_____

## 创建插件

> ![image-20250424145323851](./Image/UE_Editor_Learn_001/image-20250424145323851.png)![image-20250424145443004](./Image/UE_Editor_Learn_001/image-20250424145443004.png)

_____

## 引入模块，为了使用`UEditorUtilityLibrary`和`UEditorAssetLibrary`

详细可以参考这个[CSDN链接：UE4模块系统详解](https://blog.csdn.net/pp1191375192/article/details/103139304/)

> ```c#
> "Blutility",
> "UnrealEd",
> ```
>
> ![image-20250424145823267](./Image/UE_Editor_Learn_001/image-20250424145823267.png)

_____

## 引入模块时，需要看下目标文件属于哪个模块和依赖关系

> 目标依赖![image-20250424150109397](./Image/UE_Editor_Learn_001/image-20250424150109397.png)![image-20250424150329698](./Image/UE_Editor_Learn_001/image-20250424150329698.png)
>
> 在模块中添加![image-20250424150414151](./Image/UE_Editor_Learn_001/image-20250424150414151.png)

------

## 修改插件中的`.uplugin`文件

> ![image-20250424152102337](./Image/UE_Editor_Learn_001/image-20250424152102337.png)
>
> ```json
> {
>     "FileVersion": 3,
>     "Version": 1,
>     "VersionName": "1.0",
>     "FriendlyName": "MyEditorTool",
>     "Description": "My Editor Tool",
>     "Category": "Other",
>     "CreatedBy": "Lilou",
>     "CreatedByURL": "",
>     "DocsURL": "",
>     "MarketplaceURL": "",
>     "SupportURL": "",
>     "CanContainContent": true,
>     "IsBetaVersion": false,
>     "IsExperimentalVersion": false,
>     "Installed": false,
>     "Modules": [
>        {
>           "Name": "MyEditorTool",
>           "Type": "Editor",
>           "LoadingPhase": "PreDefault"
>        }
>     ]
> }
> ```
>
> 

------

## Generate编译

> <img src="./Image/UE_Editor_Learn_001/image-20250424145555451.png" alt="image-20250424145555451" style="zoom:50%;" />
>
> 

_____
