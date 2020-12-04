---
description: “即时开启”一词指预载一个或多个渠道，以便用户选择渠道或切换渠道时可立即看到内容播放。 缓冲已在用户开始观看时完成。
seo-description: “即时开启”一词指预载一个或多个渠道，以便用户选择渠道或切换渠道时可立即看到内容播放。 缓冲已在用户开始观看时完成。
seo-title: 即时启动
title: 即时启动
uuid: 4cb4d221-170f-46e8-af26-32f259377617
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# 即时打开{#instant-on}

“即时开启”一词指预载一个或多个渠道，以便用户选择渠道或切换渠道时可立即看到内容播放。 缓冲已在用户开始观看时完成。

如果不立即打开，TVSDK将初始化要播放的媒体，但直到应用程序调用`play`，才会开始缓冲流。 在缓冲完成之前，用户看不到任何内容。 借助即时启动，您可以启动多媒体播放器（或媒体播放器项目加载器）实例，TVSDK开始会立即缓冲流。

当用户更改渠道且流已正确缓冲时，请立即在新渠道开始上调用`play`。

尽管TVSDK可以运行的`MediaPlayer`实例数没有限制，但运行更多实例会消耗更多资源。 应用程序性能可能受运行实例数的影响。 有关这些实例的详细信息，请参阅[使用MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md)加载媒体资源。

## 为即时播放配置缓冲{#configure-buffering-for-instant-on-playback}

借助即时启动，用户可以立即切换渠道和播放开始，无需等待时间。 启用即时启用时，TVSDK会在播放开始前缓冲一个或多个渠道。

1. 通过验证状态是否为PREPARED，确认已加载资源并准备好进行播放。
1. 在调用`play`之前，请调用每个`MediaPlayer`实例的`prepareBuffer`。

   这将启用即时启用，这意味着TVSDK开始缓冲而不实际播放媒体资源。 当缓冲区已满时，TVSDK将调度`BUFFERING_COMPLETED`事件。

   >[!NOTE]
   >
   >默认情况下，`prepareBuffer`和`prepareToPlay`将媒体流设置为从头开始开始播放。 要在另一个位置开始，请将该位置（以毫秒为单位）传递到`prepareToPlay`。

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

1. 当您收到`BUFFERING_COMPLETE`事件时，开始播放项目或显示可视反馈以指示内容已完全缓冲。

   如果调用`play`，应立即开始播放。

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
