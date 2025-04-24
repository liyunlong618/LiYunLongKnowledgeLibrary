___________________________________________________________________________________________
#### [GoMenu](../UE_EditorMenu.md)
___________________________________________________________________________________________
# 005 右下角发送自定义消息
___________________________________________________________________________________________


## 目录

[TOC]

_____

## `FUdpMessageSegmenter.cpp`源码

> ```cpp
> // FUdpMessageSegmenter.cpp
> /**
>  * Adds a floating notification
>  * @param Info     Contains various settings used to initialize the notification
>  */
> SLATE_API TSharedPtr<SNotificationItem> AddNotification(const FNotificationInfo& Info);
> ```
>
> 使用示例
>
> ```cpp
> FNotificationInfo Info(TEXT("成功创建对象"));
> Info.FadeOutDuration = FadeOutDuration;
> FSlateNotificationManager::Get().AddNotification(Info);
> ```
>
> - **`FNotificationInfo`**中的常用配置修改
>
> ```CPP
>    Info.ExpireDuration = 5.0f;  // 总显示时间（秒）
>    Info.FadeInDuration = 0.2f;  // 淡入动画时长
>    Info.FadeOutDuration = 1.0f; // 淡出动画时长
>    Info.bUseLargeFont = true;       // 启用大标题字体
>    Info.Image = FCoreStyle::Get().GetBrush("SuccessIcon"); // 内置图标
>    Info.bUseThrobber = true;        // 显示加载旋转图标
> 
> // 按钮操作
>    Info.ButtonDetails.Add(
>        FNotificationButtonInfo(
>            FText::FromString("查看日志"),
>            FText::FromString("打开日志文件"),
>            FSimpleDelegate::CreateLambda([](){ /* 点击逻辑 */ })
>        )
>    );
> 
> // 超链接
>    Info.Hyperlink = FSimpleDelegate::CreateLambda([](){ 
>        FPlatformProcess::LaunchURL(TEXT("https://unrealengine.com"), nullptr, nullptr);
>    });
>    Info.HyperlinkText = FText::FromString("官方文档");
> 
> // 进度条集成
>    TSharedPtr<SProgressBar> ProgressBar = SNew(SProgressBar).Percent(0.5f);
>    Info.ContentWidget = ProgressBar; // 替换默认文本为自定义Widget
> 
> // 延迟触发
>    Info.bFireAndForget = true;
>    Info.ExpireDuration = 10.0f;
>    Info.bUseAsyncFadeOut = true; // 后台线程处理淡出
> ```
>

_____

## `DebugHeader.h`中封装功能`FSlateNotificationManager::AddNotification`

> ```cpp
> inline void SendNotification(const FString& Message, const float& FadeOutDuration = 7.f)
> {
>     FNotificationInfo Info(FText::FromString(Message));
>     Info.FadeOutDuration = FadeOutDuration;
>     FSlateNotificationManager::Get().AddNotification(Info);
> }
> ```

_____

## 创建成功时调用

> ```cpp
> void UQuickAssetAction::DuplicateAssets(int32 DuplicateNum)
> {
>     if (DuplicateNum <= 0)
>     {
>        SendMsgDiaLog(EAppMsgType::Ok, TEXT("数量必须大于0"));
>        return;
>     }
>     TArray<FAssetData> SelectedAssetData = UEditorUtilityLibrary::GetSelectedAssetData();
>     uint32 Counter = 0;
>     for (const FAssetData& Data : SelectedAssetData)
>     {
>        for (int i = 0; i < DuplicateNum; ++i)
>        {
>           const FString SourceAssetPath = Data.GetSoftObjectPath().ToString();
>           const FString NewDuplicateName = Data.AssetName.ToString() + TEXT("_") + FString::FromInt(i + 1);
>           const FString NewPathName = FPaths::Combine(Data.PackagePath.ToString(), NewDuplicateName);
> 
>           if (UEditorAssetLibrary::DuplicateAsset(SourceAssetPath, NewPathName))
>           {
>              SendNotification(TEXT("成功创建对象[ ") + NewDuplicateName + TEXT(" ]"));
>              ++Counter;
>           }
>           else
>           {
>              SendNotification(TEXT("创建对象[ ") + NewDuplicateName + TEXT(" ] 失败"));
>           }
>        }
>     }
>     if (Counter > 0)
>     {
>        Print(TEXT("成功创建对象[ ") + FString::FromInt(Counter) + TEXT(" ]个"), FColor::Green);
>        PrintLog(TEXT("成功创建对象[ ") + FString::FromInt(Counter) + TEXT(" ]个"));
>     }
> }
> ```

_____
