---
description: 要使隐藏式字幕对客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。
seo-description: 要使隐藏式字幕对客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。
seo-title: 显示隐藏式字幕
title: 显示隐藏式字幕
uuid: 7057014a-b14a-4790-8f7f-37d7a1fb8194
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 显示隐藏式字幕{#expose-closed-captions}

要使隐藏式字幕对客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。

要显示隐藏式字幕，请执行以下操作：

1. 在`PTMediaPlayer`对象中，设置`closedCaptionDisplayEnabled`属性。

   如果用户已启用隐藏式字幕，则此步骤将显示文本。

   >[!NOTE]
   >
   >客户端用户使用“iOS辅助功能设置”打开或关闭关闭的字幕，这些设置还提供格式选项。

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 属性已弃用。使用`PTMediaPlayerItem`的`subtitlesOptions`属性。 请参阅[显示字幕](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md)以使用隐藏式字幕。