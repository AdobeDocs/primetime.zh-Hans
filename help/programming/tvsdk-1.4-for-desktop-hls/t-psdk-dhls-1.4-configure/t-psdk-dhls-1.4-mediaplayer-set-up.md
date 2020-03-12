---
description: MediaPlayer界面封装媒体播放器的功能和行为。
seo-description: MediaPlayer界面封装媒体播放器的功能和行为。
seo-title: 设置MediaPlayer
title: 设置MediaPlayer
uuid: 4b27643c-9ccd-4abb-9793-475d06ee2a88
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# 设置MediaPlayer {#set-up-the-mediaplayer}

TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。

使用平台的工具创建播放器并将其连接到TVSDK中的媒体播放器视图，该视图具有播放和管理视频的方法。 例如，TVSDK提供播放和暂停方法。 您可以在平台上创建用户界面按钮并设置这些按钮以调用这些TVSDK方法。MediaPlayer界面封装媒体播放器的功能和行为。

TVSDK提供界面的单一实 `MediaPlayer` 现：defaultMediaPlayer类。 当您需要视频播放功能时，请实例化 `DefaultMediaPlayer`。

>[!NOTE]
>
>仅与实例 `DefaultMediaPlayer` 交互，并使用界面公开的方 `MediaPlayer` 法。

1. 使用应用 `MediaPlayerContext` 程序加载的实例实 `authorizedFeatures` 例化一个实例(请参 [阅加载已签名的令牌](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md))。

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. 使用公 `MediaPlayer` 共创建工厂方法实例化，传递上下文 `MediaPlayerContext` 对象：

   ```
   public static function create(context:Context):MediaPlayer
   ```

   这将返回通用 `MediaPlayer` 界面。 1.实例化 `MediaPlayerView` 并指定要使用的StageVideo实例：

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. 将实例 `MediaPlayerView` 与新创建的视图关联：

   ```
   mediaPlayer.view = view;
   ```

1. 将实 `MediaPlayerView` 例放在设备的屏幕上：

   ```
   container.addChild(view)
   ```

该实 `MediaPlayer` 例现已可用，并且已正确配置以在设备屏幕上显示视频内容。