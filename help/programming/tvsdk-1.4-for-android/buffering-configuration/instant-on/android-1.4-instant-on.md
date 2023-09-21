---
description: 术语“即时打开”是指预加载一个或多个频道，以便选择频道或切换频道的用户看到内容立即播放。 到用户开始观看时，缓冲已完成。
title: 即时打开
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 即时打开 {#instant-on}

术语“即时打开”是指预加载一个或多个频道，以便选择频道或切换频道的用户看到内容立即播放。 到用户开始观看时，缓冲已完成。

如果没有立即打开，TVSDK将初始化要播放的媒体，但在应用程序调用之前不会开始缓冲流 `play`. 在缓冲完成之前，用户不会看到任何内容。 在instant on下，您可以启动多个媒体播放器（或媒体播放器项目加载器）实例，TVSDK将立即开始缓冲流。

当用户更改频道且流已正确缓冲时，调用 `play` 在新的频道上立即开始播放。

尽管数量并无限制，但 `MediaPlayer` TVSDK可以运行的实例，运行更多实例会占用更多资源。 运行的实例数可能会影响应用程序性能。 有关这些实例的详细信息，请参阅 [使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## 为即时播放配置缓冲 {#configure-buffering-for-instant-on-playback}

即时打开时，用户可以切换频道，并且立即开始播放，而无需等待时间。 启用“即时打开”后，TVSDK会在开始播放之前缓冲一个或多个通道。

1. 通过验证状态是否为PREPARED，确认资源已加载并准备好播放。
1. 呼叫前 `play`，调用 `prepareBuffer` 每个 `MediaPlayer` 实例。

   这样可启用即时打开，这意味着TVSDK开始缓冲而不实际播放媒体资源。 TVSDK调度 `BUFFERING_COMPLETED` 缓冲区已满时的事件。

   >[!NOTE]
   >
   >默认情况下， `prepareBuffer` 和 `prepareToPlay` 设置媒体流以从头开始播放。 要从另一个位置开始，请将该位置（以毫秒为单位）传递到 `prepareToPlay`.

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

1. 当您收到 `BUFFERING_COMPLETE` 事件，开始播放该项目或显示可视化反馈以指示内容已完全缓冲。

   如果您致电 `play`，应立即开始播放。

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
