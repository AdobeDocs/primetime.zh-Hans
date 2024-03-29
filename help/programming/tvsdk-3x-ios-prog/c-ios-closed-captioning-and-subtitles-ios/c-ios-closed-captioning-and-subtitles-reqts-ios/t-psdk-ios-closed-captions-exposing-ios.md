---
description: 要使隐藏式字幕对客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。
title: 公开隐藏字幕
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 公开隐藏字幕 {#expose-closed-captions}

要使隐藏式字幕对客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。

要显示隐藏式字幕，请执行以下操作：

1. 在 `PTMediaPlayer` 对象，设置 `closedCaptionDisplayEnabled` 属性。

   如果用户启用了隐藏式字幕，则此步骤将显示文本。

   >[!NOTE]
   >
   >客户端用户通过使用iOS辅助功能设置来打开或关闭隐藏式字幕，并且这些设置还提供了格式选项。

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 属性已弃用。 使用 `subtitlesOptions` 属性 `PTMediaPlayerItem`. 请参阅 [公开字幕](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) 使用隐藏式字幕。
