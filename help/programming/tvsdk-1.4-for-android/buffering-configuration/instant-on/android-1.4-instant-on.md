---
description: “即时启用”是指预载一个或多个渠道，以便用户选择渠道或切换渠道时可立即看到内容播放。 缓冲已在用户开始观看时完成。
title: 即时启动
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# 在{#instant-on}上即时

“即时启用”是指预载一个或多个渠道，以便用户选择渠道或切换渠道时可立即看到内容播放。 缓冲已在用户开始观看时完成。

如果不立即打开，TVSDK将初始化要播放的媒体，但在应用程序调用`play`之前不开始缓冲流。 在缓冲完成之前，用户看不到任何内容。 借助即时启动，您可以启动多媒体播放器（或媒体播放器项目加载器）实例，TVSDK开始会立即缓冲流。

当用户更改渠道且流已正确缓冲时，将立即在新渠道开始播放时调用`play`。

尽管TVSDK可以运行的`MediaPlayer`实例数没有限制，但运行更多实例会消耗更多资源。 应用程序性能可能受运行实例数的影响。 有关这些实例的详细信息，请参阅[使用MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md)加载媒体资源。

## 为即时播放配置缓冲{#configure-buffering-for-instant-on-playback}

借助即时启用，用户可以立即切换渠道和播放开始，而无需等待时间。 启用即时启用时，TVSDK会在播放开始前缓冲一个或多个渠道。

1. 通过验证状态是否为PREPARED，确认资源已加载并准备好播放。
1. 在调用`play`之前，请为每个`MediaPlayer`实例调用`prepareBuffer`。

   这将启用即时启动，这意味着TVSDK开始在不实际播放媒体资源的情况下进行缓冲。 当缓冲区已满时，TVSDK将调度`BUFFERING_COMPLETED`事件。

   >[!NOTE]
   >
   >默认情况下，`prepareBuffer`和`prepareToPlay`将媒体流设置为从开头开始播放的开始。 要在另一个位置开始，请将该位置（以毫秒为单位）传递到`prepareToPlay`。

   ```java
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state,  
                              MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               // By default, prepareToPlay and prepareBuffer buffer and start playing 
               // from the beginning of the stream. To start at another position, 
               // pass it into prepareToPlay. This example starts 5 seconds into the stream. 
               _mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               _mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. 当您收到`BUFFERING_COMPLETE`事件时，播放项目的开始或显示可视反馈以指示内容已完全缓冲。

   如果调用`play`，应立即开始播放。

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
