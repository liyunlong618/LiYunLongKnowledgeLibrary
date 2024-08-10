___________________________________________________________________________________________
# UE中的常用宏
___________________________________________________________________________________________


## 目录

[TOC]

___________________________________________________________________________________________

### UE_LOG

<details>
<summary>UE_LOG宏介绍</summary>

> - 头文件片段的语法是DECLARE_LOG_CATEGORY_EXTERN(CategoryName, DefaultVerbosity, CompileTimeVerbosity). DefaultVerbosity 是在 ini 文件或命令行中未指定详细级别时使用的详细级别。不会记录任何比这更详细的内容。CompileTimeVerbosity 是要在代码中编译的最大详细程度。任何比这更详细的内容都不会被编译。  

</details>


- UE_LOG宏使用
  使用时在头文件或者源文件都可

  ```CPP
     DECLARE_LOG_CATEGORY_EXTERN(这里是自定义log名字, error, All);
  ```

- 参考网页

  [知乎——虚幻UE_LOG使用教程](https://zhuanlan.zhihu.com/p/463724067)



## UEC++中使用`GEngine`将消息打印到屏幕

<details>
<summary>介绍</summary>

> - 第一个参数是消息的键（key）。如果 key 设置为 -1，则每次执行这行代码时，都会在屏幕上添加一条新消息。例如，如果将这个添加到Tick()函数中，屏幕很快就会充斥着这些消息流。如果键是正整数（键的类型是 uint64），则每条新消息都会用与其键相同的整数替换前一条消息。例如，如果调用上述函数Tick()并将其键修改为 1，则游戏中的屏幕上只会看到一条消息，因为每个新调用都会简单地替换它。  
> - 第二个参数是显示消息的时长，以秒为单位，它是浮点类型。  
> - 第三个参数是一个FColor 类型的参数，用来确定文本颜色。最好使用在游戏世界背景下易于阅读的颜色。最简单的方法是使用预定义的颜色常量，例如FColor::White. 有关可用颜色常量的完整列表，请参阅[此官方文档页面](https://link.zhihu.com/?target=https%3A//docs.unrealengine.com/en-US/API/Runtime/Core/Math/FColor/index.html)的底部。  
> - 第四个参数是消息本身。请注意，整个字符串必须只占用一个参数，因此，有多个参数的情况下需要使用FString::Printf()：  
> - GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Red, FString::Printf(TEXT("Some variable values: x = %f, y = %f"), x, y));  
> - AddOnScreenDebugMessage()还有两个可选参数。第五个参数是一个布尔值，用于确定新消息是出现在顶部（如果为真）还是底部（如果为假）。请注意，这仅适用于键值设置为 -1 的情况。第六个参数是确定文本比例的二维向量。如果打印到屏幕上的消息太小而难以阅读，或者它们太大并占用太多屏幕空间，这将非常有用。  
> - Visual Studio 可能会在 GEngine 下划线并声称它是未定义的。但是，你无需显式包含 Engine.h 或 EngineGlobals.h 即可在任何类中使用它。尽管有红色下划线，它应该可以编译并正常工作。
>
> 源码：![](./Image/CommonMacrosUE/1.png)

</details>

```CPP
GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::White, TEXT("This message will appear on the screen!"));
```

