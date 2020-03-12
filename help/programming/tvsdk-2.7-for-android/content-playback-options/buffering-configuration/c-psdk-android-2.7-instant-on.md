---
description: 即时启用意味着预加载了一个或多个渠道。 当用户选择渠道或切换渠道时，内容会立即播放。 缓冲在用户开始观看时完成。
seo-description: 即时启用意味着预加载了一个或多个渠道。 当用户选择渠道或切换渠道时，内容会立即播放。 缓冲在用户开始观看时完成。
seo-title: 即时打开
title: 即时打开
uuid: 7e14b779-2a36-4ff4-a365-9ac49a836ff3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# 即时打开 {#instant-on}

即时启用意味着预加载了一个或多个渠道。 当用户选择渠道或切换渠道时，内容会立即播放。 缓冲在用户开始观看时完成。

如果没有“即时打开”,TVSDK将初始化要播放的媒体，但直到应用程序调用时才开始缓冲流 `play`。 在缓冲完成之前，用户不会看到任何内容。 借助“即时开启”，您可以启动多媒体播放器（或媒体播放器项目加载器）实例，TVSDK会立即开始缓冲流。 当用户更改频道且流已正确缓冲时，对新频道 `play` 的调用会立即开始播放。

尽管对TVSDK可以运行的实例数 `MediaPlayer` 和实 `MediaPlayerItemLoader` 例数没有限制，但运行更多实例会消耗更多资源。 应用程序性能可能受正在运行的实例数的影响。 有关详细信息， `MediaPlayerItemLoader`请参阅 [在媒体播放器中加载媒体资源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md)。

>[!IMPORTANT]
>
>TVSDK不支持同时使用 `QoSProvider` 和的单个 `itemLoader` 软件 `MediaPlayer`。 如果客户使用即时启动，则应用程序需要维护两个QoS实例并管理两个实例以获取相关信息。

有关详细信息， `MediaPlayerItemLoader`请参 [阅使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md)。

## 将QoS提供者实例添加到mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* 创建QoS提供者并将其连接到实 `mediaPlayerItemLoader` 例

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   播放开始后，使用 `_qosProvider` 获取和 `timeToLoad` QoS `timeToPrepare` 数据。 剩余的QoS度量可以通过使用附加到 `QoSProvider` 的来检索 `mediaPlayer`。

   有关详细信息， `MediaPlayerItemLoader`请参 [阅使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader)。

## 为“即时打开”配置缓冲 {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK提供了允许您对媒体资源使用“即时打开”的方法和状态。

>[!NOTE]
>
>Adobe建议使用 `MediaPlayerItemLoader` 于InstantOn。 要使用( `MediaPlayerItemLoader`而非 `MediaPlayer`)media-resource-load-using-mediaplayeritemloader，请参阅media-resource-load-using-mediaplayeritemloader。

1. 确认已加载资源，且播放器准备播放该资源。
1. 在调用之 `play`前，请调 `prepareBuffer` 用每个 `MediaPlayer` 实例。

   >[!NOTE]
   >
   >`prepareBuffer` 启用“即时开启”,TVSDK会立即开始缓冲，并 `BUFFERING_COMPLETED` 在缓冲区已满时调度事件。

   >[!TIP]
   >
   >默认情况 `prepareBuffer` 下， `prepareToPlay` 将媒体流设置为从头开始播放。 要从另一个位置开始，请将该位置（以毫秒为单位）传递到 `prepareToPlay`。

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

1. 当您收到该事 `BUFFERING_COMPLETE` 件时，开始播放该项目或显示可视反馈以指示内容已完全缓冲。

   >[!NOTE]
   >
   >如果拨叫， `play`应立即开始播放。

