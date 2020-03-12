---
description: 要使隐藏式字幕对您的客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。
seo-description: 要使隐藏式字幕对您的客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。
seo-title: 显示隐藏式字幕
title: 显示隐藏式字幕
uuid: 209b34ca-f14e-499e-af5f-2d8c7b359ef8
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b

---


# 显示隐藏式字幕 {#expose-closed-captions}

要使隐藏式字幕对您的客户端播放器可用，必须启用它们。 用户可以打开或关闭隐藏式字幕并选择格式。

要显示隐藏式字幕，请执行以下操作：

1. 在对 `PTMediaPlayer` 象中，设置属 `closedCaptionDisplayEnabled` 性。

   如果用户已启用隐藏式字幕，则此步骤将显示文本。

   >[!NOTE]
   >
   >客户端用户使用“iOS辅助功能设置”打开或关闭关闭的字幕，这些设置还提供格式选项。

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 属性已弃用。 使用 `subtitlesOptions` 属性 `PTMediaPlayerItem`。 请参 [阅显示字幕](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) ，以使用隐藏式字幕。