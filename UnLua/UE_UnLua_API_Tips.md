___________________________________________________________________________________________
###### [GoLibraryMainMenu](../_LibraryMainMenu_.md)
___________________________________________________________________________________________
# UE  Lua插件 `UnLua` 的使用方法


___________________________________________________________________________________________

[TOC]

------

## TODO 这里先记录

------

## 使用`.`和`:`调用函数
区别为使用`.`需要传self作为首个参数(因为蓝图调用对象也需要实例来调用)
```Lua
function M:PrintLog()
    print("SomeLog")
end
-- . 调用 需显式传入 self(首个参数)
M.PrintLog(self)
-- : 调用 自动传入 self(无需显式写出)
M:PrintLog()

```
------

## 使用UE得数据类型需要用到UE的对象
比如
```Lua
local Brush = UE.FSlateBrush()

```
------

## 调用时遵循蓝图的调用参数，而不是cpp的

比如调用蓝图的`PrintString`

虽然cpp中需要第一个参数传`WorldContextObject`但是因为蓝图这里自动给了this，所以不用传

下面这个第一个参数传`this`，是因为`lua`方法`.`调用
如果换成`:`调用就不用传`self`

```lua
UE.UKismetSystemLibrary.PrintString(self, "TileDragDropIcon 构造完成，红色提示", true, true, UE.FLinearColor(1, 0, 0, 1), 5.0, "None")
```

------

## 使用local 函数内声明函数
```Lua
-- 根据材质修改按钮
function M:SetButtonMaterial(DyanmicMaterialInstance)
    print("IsValid(DyanmicMaterialInstance)", UE.UObject.IsValid(DyanmicMaterialInstance))

    local ButtonSize = UE.FVector2D(100, 100)

    local function CreateMaterialBrush(Material, Size)
        local Brush = UE.FSlateBrush()
        Brush.ResourceObject = Material
        Brush.ImageSize = Size
        Brush.DrawAs = UE.ESlateBrushDrawType.Image
        return Brush
    end

    local FButtonStyle = UE.FButtonStyle()
    FButtonStyle.Normal = CreateMaterialBrush(DyanmicMaterialInstance, ButtonSize)
    FButtonStyle.Hovered = CreateMaterialBrush(DyanmicMaterialInstance, ButtonSize)
    FButtonStyle.Pressed = CreateMaterialBrush(DyanmicMaterialInstance, ButtonSize)
    FButtonStyle.Disabled = CreateMaterialBrush(DyanmicMaterialInstance, ButtonSize)

    self.Button_28:SetStyle(FButtonStyle)
end
```