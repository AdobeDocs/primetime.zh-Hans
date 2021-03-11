---
description: MediaPlayer界面封装媒体播放器的功能和行为。
title: 设置MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# 设置MediaPlayer {#set-up-the-mediaplayer}

TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将该应用程序与其他Primetime组件集成。

使用您平台的工具创建播放器并将其连接到TVSDK中的媒体播放器视图,TVSDK中有播放和管理视频的方法。 例如，TVSDK提供播放和暂停方法。 您可以在平台上创建用户界面按钮并设置按钮以调用这些TVSDK方法。MediaPlayer界面封装媒体播放器的功能和行为。

TVSDK提供`MediaPlayer`接口的单个实现：DefaultMediaPlayer类。 当您需要视频播放功能时，请实例化`DefaultMediaPlayer`。

>[!NOTE]
>
>仅与`MediaPlayer`接口公开的方法与`DefaultMediaPlayer`实例交互。

1. 使用应用程序加载的`authorizedFeatures`实例实例化`MediaPlayerContext`（请参阅[加载已签名的令牌](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)）。

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. 使用公共创建工厂方法实例化`MediaPlayer`，传递`MediaPlayerContext`上下文对象：

   ```
   public static function create(context:Context):MediaPlayer
   ```

   这将返回通用`MediaPlayer`接口。 1.实例化`MediaPlayerView`并指定要使用的StageVideo实例：

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. 将`MediaPlayerView`实例与新创建的视图关联：

   ```
   mediaPlayer.view = view;
   ```

1. 将`MediaPlayerView`实例放在设备的屏幕上：

   ```
   container.addChild(view)
   ```

`MediaPlayer`实例现已可用，并已正确配置以在设备屏幕上显示视频内容。