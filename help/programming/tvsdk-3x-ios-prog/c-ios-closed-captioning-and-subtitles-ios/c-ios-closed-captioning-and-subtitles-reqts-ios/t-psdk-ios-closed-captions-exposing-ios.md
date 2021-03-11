---
description: 要使隐藏式字幕对您的客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。
title: 显示隐藏式字幕
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# 显示隐藏式字幕{#expose-closed-captions}

要使隐藏式字幕对您的客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。

显示隐藏式字幕：

1. 在`PTMediaPlayer`对象中，设置`closedCaptionDisplayEnabled`属性。

   如果用户已启用隐藏式字幕，则此步骤将显示文本。

   >[!NOTE]
   >
   >客户端用户使用iOS“辅助功能设置”打开或关闭关闭的字幕，这些设置还提供格式选项。

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 属性已弃用。使用`PTMediaPlayerItem`的`subtitlesOptions`属性。 请参阅[显示字幕](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md)以使用隐藏式字幕。