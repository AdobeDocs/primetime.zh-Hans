---
description: “即时开启”一词指预加载一个或多个渠道，以便用户选择渠道或切换渠道后可立即看到内容播放。 缓冲在用户开始观看时已完成。
seo-description: “即时开启”一词指预加载一个或多个渠道，以便用户选择渠道或切换渠道后可立即看到内容播放。 缓冲在用户开始观看时已完成。
seo-title: 即时启动
title: 即时启动
uuid: 4cb4d221-170f-46e8-af26-32f259377617
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 即时启动 {#instant-on}

“即时开启”一词指预加载一个或多个渠道，以便用户选择渠道或切换渠道后可立即看到内容播放。 缓冲在用户开始观看时已完成。

在不立即打开的情况下，TVSDK将初始化要播放的媒体，但直到应用程序调用时才开始缓冲流 `play`。 在缓冲完成之前，用户不会看到任何内容。 即时启动后，您可以启动多媒体播放器（或媒体播放器项目加载器）实例，TVSDK会立即开始缓冲流。

当用户更改频道且流已正确缓冲时，对新频道 `play` 的调用会立即开始播放。

尽管对TVSDK可以运行的实例数 `MediaPlayer` 量没有限制，但运行更多实例会占用更多资源。 应用程序性能可能受运行实例数的影响。 有关这些实例的详细信息，请参 [阅使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md)。

## 为即时播放配置缓冲 {#configure-buffering-for-instant-on-playback}

即时开启后，用户可以切换频道并立即开始播放，无需等待时间。 当您启用即时打开时，TVSDK会在播放开始前缓冲一个或多个频道。

1. 确认资源已加载并已准备好播放，方法是确认状态为PREPARED。
1. 在调用之 `play`前，请调 `prepareBuffer` 用每个 `MediaPlayer` 实例。

   这将启用即时启动，这意味着TVSDK开始缓冲而不实际播放媒体资源。 TVSDK在缓冲 `BUFFERING_COMPLETED` 区已满时调度该事件。

   >[!NOTE]
   >
   >默认情况 `prepareBuffer` 下， `prepareToPlay` 将媒体流设置为从头开始播放。 要从另一个位置开始，请将该位置（以毫秒为单位）传递到 `prepareToPlay`。

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

1. 当您收到该事 `BUFFERING_COMPLETE` 件时，开始播放该项目或显示可视反馈以指示内容已完全缓冲。

   如果拨叫， `play`应立即开始播放。

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
