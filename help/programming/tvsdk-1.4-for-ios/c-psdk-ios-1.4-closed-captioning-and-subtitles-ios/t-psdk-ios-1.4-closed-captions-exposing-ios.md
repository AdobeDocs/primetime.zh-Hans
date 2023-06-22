---
description: 要使隐藏式字幕对客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。
title: 公开隐藏字幕
exl-id: 57168c6e-a958-4a89-b22b-0c9f1cab3a49
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 公开隐藏字幕 {#expose-closed-captions}

要使隐藏式字幕对客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。

要显示隐藏式字幕，请执行以下操作：

1. In `PTMediaPlayer` 对象，设置 `closedCaptionDisplayEnabled` 属性。

   如果用户启用了隐藏式字幕，则此步骤将显示文本。

   >[!NOTE]
   >
   >客户端用户可使用iOS辅助功能设置打开或关闭隐藏式字幕，这些设置还提供了格式选项。

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 属性已弃用。 使用 `subtitlesOptions` 属性 `PTMediaPlayerItem`. 参见 [公开字幕](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) 使用隐藏式字幕。
