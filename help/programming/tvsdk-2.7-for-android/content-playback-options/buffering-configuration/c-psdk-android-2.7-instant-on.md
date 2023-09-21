---
description: 启用“立即打开”表示预加载一个或多个通道。 当用户选择渠道或切换渠道时，内容会立即播放。 到用户开始观看时，缓冲结束。
title: 即时打开
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 即时打开 {#instant-on}

启用“立即打开”表示预加载一个或多个通道。 当用户选择渠道或切换渠道时，内容会立即播放。 到用户开始观看时，缓冲结束。

如果没有打开即时，TVSDK将初始化要播放的媒体，但在应用程序调用之前不会开始缓冲流 `play`. 在缓冲完成之前，用户不会看到任何内容。 利用Instant On，您可以启动多个媒体播放器（或媒体播放器项目加载器）实例，TVSDK将立即开始缓冲流。 当用户更改频道且流已正确缓冲时，调用 `play` 在新的频道上立即开始播放。

尽管数量并无限制，但 `MediaPlayer` 和 `MediaPlayerItemLoader` TVSDK可以运行的实例，运行更多实例会占用更多资源。 应用程序的性能可能会受正在运行的实例数影响。 有关详情 `MediaPlayerItemLoader`，请参见 [在媒体播放器中加载媒体资源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK不支持单个 `QoSProvider` 以同时使用两者 `itemLoader` 和 `MediaPlayer`. 如果客户使用Instant On，则应用程序需要维护两个QoS实例并管理这两个实例来获取信息。

有关详情 `MediaPlayerItemLoader`，请参见 [使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

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

  有关详情 `MediaPlayerItemLoader`，请参见 [使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader).

## 为即时打开配置缓冲 {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK提供了方法和状态，允许您将“即时开启”与媒体资源一起使用。

>[!NOTE]
>
>Adobe建议使用 `MediaPlayerItemLoader` 用于InstantOn。 使用 `MediaPlayerItemLoader`，而不是 `MediaPlayer`，请参阅media-resource-load-using-mediaplayeritemloader 。

1. 确认资源已加载，并且播放器已准备好播放该资源。
1. 呼叫前 `play`，调用 `prepareBuffer` 每个 `MediaPlayer` 实例。

   >[!NOTE]
   >
   >`prepareBuffer` 启用Instant On，TVSDK立即开始缓冲并调度 `BUFFERING_COMPLETED` 缓冲区已满时的事件。

   >[!TIP]
   >
   >默认情况下， `prepareBuffer` 和 `prepareToPlay` 设置媒体流以从头开始播放。 若要从另一个位置开始，请将该位置（以毫秒为单位）传递给 `prepareToPlay`.

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

1. 当您收到 `BUFFERING_COMPLETE` 事件，开始播放该项目或显示可视化反馈以指示内容已完全缓冲。

   >[!NOTE]
   >
   >如果您致电 `play`，应立即开始播放。
