---
description: 启用即时启用意味着预加载一个或多个渠道。 当用户选择渠道或切换渠道时，内容将立即播放。 缓冲在用户开始观看时完成。
seo-description: 启用即时启用意味着预加载一个或多个渠道。 当用户选择渠道或切换渠道时，内容将立即播放。 缓冲在用户开始观看时完成。
seo-title: 即时启动
title: 即时启动
uuid: 5b1ceace-cae7-44c7-b4b9-d45078d58cc3
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# 即时打开{#instant-on}

启用即时启用意味着预加载一个或多个渠道。 当用户选择渠道或切换渠道时，内容将立即播放。 缓冲在用户开始观看时完成。

如果没有“即时打开”,TVSDK将初始化要播放的媒体，但直到应用程序调用`play`时才开始缓冲流。 在缓冲完成之前，用户看不到任何内容。 借助“即时开启”，您可以启动多媒体播放器（或媒体播放器项目加载器）实例，并且TVSDK开始可立即缓冲流。 当用户更改渠道且流已正确缓冲时，请立即在新渠道开始上调用`play`。

尽管对TVSDK可以运行的`MediaPlayer`和`MediaPlayerItemLoader`实例数没有限制，但运行更多实例会消耗更多资源。 应用程序性能可能受正在运行的实例数的影响。 有关`MediaPlayerItemLoader`的详细信息，请参阅[在媒体播放器中加载媒体资源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md)。

>[!IMPORTANT]
>
>TVSDK不支持单个`QoSProvider`以同时与`itemLoader`和`MediaPlayer`一起使用。 如果客户使用“即时启动”，则应用程序需要维护两个QoS实例并管理两个实例以获取信息。

有关`MediaPlayerItemLoader`的详细信息，请参阅[使用MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md)加载媒体资源。

## 将QoS提供者实例添加到mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* 创建QoS提供程序并将其连接到`mediaPlayerItemLoader`实例

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   播放开始后，使用`_qosProvider`获取`timeToLoad`和`timeToPrepare` QoSdata。 剩余的QoS度量可通过使用附加到`mediaPlayer`的`QoSProvider`来检索。

   有关`MediaPlayerItemLoader`的详细信息，请参阅[使用MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md)加载媒体资源。

## 为“在{#section_4FE346B7BE434BA8A2203896D6E52146}上即时”配置缓冲

TVSDK提供允许您对媒体资源使用“即时打开”的方法和状态。

>[!NOTE]
>
>Adobe建议对InstantOn使用`MediaPlayerItemLoader`。 要使用`MediaPlayerItemLoader`而不是`MediaPlayer`，请参阅[使用MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md)加载媒体资源。

1. 确认已加载资源，且播放器已准备好播放该资源。
1. 在调用`play`之前，请调用每个`MediaPlayer`实例的`prepareBuffer`。

   `prepareBuffer` 启用“即时打开”,TVSDK开始立即进行缓冲，并 `BUFFERING_COMPLETED` 在缓冲区已满时分派事件。

   >[!TIP]
   >
   >默认情况下，`prepareBuffer`和`prepareToPlay`将媒体流设置为从头开始开始播放。 要在另一个位置开始，请将该位置（以毫秒为单位）传递到`prepareToPlay`。

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

1. 当您收到`BUFFERING_COMPLETE`事件时，开始播放项目或显示可视反馈以指示内容已完全缓冲。

   >[!NOTE]
   >
   >如果调用`play`，应立即开始播放。