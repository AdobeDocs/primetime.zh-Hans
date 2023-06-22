---
description: 启用instant on表示预加载一个或多个通道。 当用户选择频道或切换频道时，内容会立即播放。 缓冲在用户开始观看时结束。
title: 即时打开
exl-id: 59293e07-160a-41a2-8ffe-7ca9323048f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 即时打开 {#instant-on}

启用instant on表示预加载一个或多个通道。 当用户选择频道或切换频道时，内容会立即播放。 缓冲在用户开始观看时结束。

如果不使用“即时打开”，TVSDK将初始化要播放的媒体，但在应用程序调用之前不会开始缓冲流 `play`. 在缓冲完成之前，用户看不到任何内容。 借助Instant On，您可以启动多个媒体播放器（或媒体播放器项目加载器）实例，并且TVSDK会立即开始缓冲流。 当用户更改频道且流已正确缓冲时，调用 `play` 在新的频道上立即开始播放。

尽管对数量没有限制 `MediaPlayer` 和 `MediaPlayerItemLoader` TVSDK可以运行的实例，运行更多实例会占用更多资源。 应用程序性能可能会受正在运行的实例数影响。 有关详情，请参阅 `MediaPlayerItemLoader`，请参见 [在媒体播放器中加载媒体资源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK不支持单个 `QoSProvider` 以同时使用两者 `itemLoader` 和 `MediaPlayer`. 如果客户使用Instant On，则应用程序需要维护两个QoS实例并管理这两个实例以获取信息。

有关详情，请参阅 `MediaPlayerItemLoader`，请参见 [使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## 将QoS提供程序实例添加到mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* 创建QoS提供商并将其附加到 `mediaPlayerItemLoader` 实例

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   开始播放后，使用 `_qosProvider` 以获取 `timeToLoad` 和 `timeToPrepare` QoSdata。 剩余的QoS量度可通过使用 `QoSProvider` 附加到 `mediaPlayer`.

   有关详情，请参阅 `MediaPlayerItemLoader`，请参见 [使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## 配置缓冲以便即时开启 {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK提供了一些方法和状态，允许您将“即时开启”与媒体资源一起使用。

>[!NOTE]
>
>Adobe建议使用 `MediaPlayerItemLoader` 用于InstantOn。 使用 `MediaPlayerItemLoader`，而不是 `MediaPlayer`，请参见 [使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. 确认资源已加载，并且播放器已准备好播放该资源。
1. 调用之前 `play`，调用 `prepareBuffer` 每个 `MediaPlayer` 实例。

   `prepareBuffer` 启用Instant On，TVSDK立即开始缓冲并调度 `BUFFERING_COMPLETED` 缓冲区已满时的事件。

   >[!TIP]
   >
   >默认情况下， `prepareBuffer` 和 `prepareToPlay` 设置媒体流以从头开始播放。 要从另一个位置开始，请将位置（以毫秒为单位）传递到 `prepareToPlay`.

   ```
   @Override 
   public void onStatusChanged(MediaPlayerStatus status) { 
       switch (status) { 
           case INITIALIZED: 
               // This example starts 5 seconds into the stream. 
               mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. 当您收到 `BUFFERING_COMPLETE` 事件，开始播放该项目或显示视觉反馈，以指示内容已完全缓冲。

   >[!NOTE]
   >
   >如果您调用 `play`，应立即开始播放。
