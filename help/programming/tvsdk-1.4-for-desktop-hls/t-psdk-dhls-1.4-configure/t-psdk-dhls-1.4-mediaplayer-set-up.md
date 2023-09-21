---
description: MediaPlayer界面封装媒体播放器的功能和行为。
title: 设置MediaPlay
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 设置MediaPlay {#set-up-the-mediaplayer}

TVSDK提供了用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。

使用您平台的工具来创建播放器，并将其连接到TVSDK中的媒体播放器视图，该视图提供了多种播放和管理视频的方法。 例如，TVSDK提供播放和暂停方法。 您可以在平台上创建用户界面按钮，并设置这些按钮以调用这些TVSDK方法。MediaPlayer界面封装了媒体播放器的功能和行为。

TVSDK可提供 `MediaPlayer` 接口： DefaultMediaPlayer类。 当您需要视频播放功能时，实例化 `DefaultMediaPlayer`.

>[!NOTE]
>
>与 `DefaultMediaPlayer` 仅使用由公开的方法的实例 `MediaPlayer` 界面。

1. 实例化 `MediaPlayerContext` 使用已加载的应用程序 `authorizedFeatures` 实例(请参阅 [加载您的签名令牌](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md))。

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. 实例化 `MediaPlayer` 使用公共create factory方法，传递 `MediaPlayerContext` 上下文对象：

   ```
   public static function create(context:Context):MediaPlayer
   ```

   这将返回一个通用 `MediaPlayer` 界面。 1.实例化a `MediaPlayerView` 并指定要使用的StageVideo实例：

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. 关联 `MediaPlayerView` 具有新创建视图的实例：

   ```
   mediaPlayer.view = view;
   ```

1. 放置 `MediaPlayerView` 设备屏幕上的实例：

   ```
   container.addChild(view)
   ```

此 `MediaPlayer` 实例现已可用，并且已正确配置为在设备屏幕上显示视频内容。
