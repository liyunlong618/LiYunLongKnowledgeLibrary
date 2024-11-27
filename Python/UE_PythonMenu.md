___________________________________________________________________________________________
###### [GoLibraryMainMenu](../_LibraryMainMenu_.md)
___________________________________________________________________________________________
# UE  Python的使用方法


___________________________________________________________________________________________


## 目录

### [UE Python中调用函数](./UE_Python/UE_Python01.md)

### [在PyCharm中支持unreal库的代码补全](./UE_Python/UE_Python02.md)

### [**UE4 Python 常用功能**](./UE_Python/UE_Python03.md)

<details>
<summary>通过 Unreal Engine 的 Python API 向编辑器添加一个自定义菜单 代码</summary>

>初始时需要加载的脚本
>
>```python
>import unreal # 加载虚幻模块
>from Vehicle import VehicleProductionSetting  # 从 Vehicle 文件夹导入模块
>
># 创建自定义菜单的方法
>def create_custom_menu():
>    # 获取菜单管理器
>    editor_utility = unreal.ToolMenus.get()
>
>    # 获取或创建主菜单
>    main_menu = editor_utility.find_menu("LevelEditor.MainMenu")
>    if not main_menu:
>        unreal.log_error("Could not find main menu!")
>        return
>
>    # 创建一个自定义菜单
>    custom_menu_name = "ProductionVehiclesSetting"
>    custom_menu = main_menu.add_sub_menu(
>        owner=main_menu.menu_name,
>        section_name="Custom",
>        name=custom_menu_name,
>        label="ProductionVehiclesSetting",
>        tool_tip="量产载具相关工具"
>    )
>
>    # 检查自定义菜单是否成功创建
>    if not custom_menu:
>        unreal.log_error("Failed to create custom menu!")
>        return
>
>    # 添加第一个子菜单按钮
>    entry_one = unreal.ToolMenuEntry(
>        name="RemoveCollisionFromSelectedAssets_Editor",
>        type=unreal.MultiBlockType.MENU_ENTRY,
>        insert_position=unreal.ToolMenuInsert("", unreal.ToolMenuInsertType.DEFAULT)
>    )
>    entry_one.set_label("RemoveCollisionFromSelectedAssets_Editor")
>    entry_one.set_tool_tip("移除选中SM资产的简单碰撞,批量设置为使用复杂碰撞(使用方法：需要选中要修改的SM资产)")
>    entry_one.set_string_command(
>        type=unreal.ToolMenuStringCommandType.PYTHON,
>        custom_type="",
>        string="from Vehicle import VehicleProductionSetting; VehicleProductionSetting.remove_collision_from_selected_assets()"
>    )
>    custom_menu.add_menu_entry("SubMenuSection", entry_one)
>
>    # 添加第二个子菜单按钮
>    entry_two = unreal.ToolMenuEntry(
>        name="SetSMToBP_Editor",
>        type=unreal.MultiBlockType.MENU_ENTRY,
>        insert_position=unreal.ToolMenuInsert("", unreal.ToolMenuInsertType.DEFAULT)
>    )
>    entry_two.set_label("SetSMToBP_Editor")
>    entry_two.set_tool_tip("通过VehicleProductionSetting中的静态表一一使用指定SM配置StaticMeshComponent(使用方法：需要选中要配置的BP和SM资产)")
>    entry_two.set_string_command(
>        type=unreal.ToolMenuStringCommandType.PYTHON,
>        custom_type="",
>        string="from Vehicle import VehicleProductionSetting; VehicleProductionSetting.set_sm_to_bp()"
>    )
>    custom_menu.add_menu_entry("SubMenuSection", entry_two)
>
>    # 刷新菜单
>    editor_utility.refresh_all_widgets()
>
># 执行创建菜单
>create_custom_menu()
>
>```
>
>因为 `set_string_command` 需要传入一个Python文件也就是模块，所以需要额外创建一个py文件
>
>```python
>import unreal
>
>
>def remove_collision_from_selected_assets():
>    unreal.log("RemoveCollisionFromSelectedAssets_Editor executed!")
>    # 实现移除碰撞逻辑
>
>    # 调用CPP静态方法
>    unreal.VehicleProductionSetting.remove_collision_from_selected_assets_editor()
>
>
>def set_sm_to_bp():
>
>    unreal.log("SetSMToBP_Editor executed!")
>
>    # 调用CPP静态方法
>    unreal.VehicleProductionSetting.set_sm_to_bp_editor()
>```
>
>这样通过初始时加载的模块，调用下面这个模块中的函数，函数中再调用cpp的静态方法（需要蓝图可调用！）

------

</details>

------

参考链接：

[ Python in UE4 哔哩哔哩_bilibili ](https://www.bilibili.com/video/BV1PE411d7z8/?spm_id_from=333.880.my_history.page.click&vd_source=9e1e64122d802b4f7ab37bd325a89e6c)