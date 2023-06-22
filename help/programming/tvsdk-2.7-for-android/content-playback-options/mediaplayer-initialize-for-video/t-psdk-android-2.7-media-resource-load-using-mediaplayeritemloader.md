---
description: 使用MediaPlayerItemLoader有助于获取有关媒体流的信息，而无需实例化MediaPlayer实例。 这在预缓冲流中尤其有用，以便可以开始无延迟的播放。
title: 使用MediaPlayerItemLoader加载媒体资源
exl-id: 6bd081bb-b92b-4c0a-a3bc-ef2128d0d8bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# 使用MediaPlayerItemLoader加载媒体资源 {#load-a-media-resource-using-mediaplayeritemloader}

使用MediaPlayerItemLoader有助于获取有关媒体流的信息，而无需实例化MediaPlayer实例。 这在预缓冲流中尤其有用，以便可以开始无延迟的播放。

此 `MediaPlayerItemLoader` 类帮助您交换当前介质的媒体资源 `MediaPlayerItem` 而不将视图附加到 `MediaPlayer` 实例，用于分配视频解码硬件资源。 对于受DRM保护的内容，需要执行其他步骤，但本手册未介绍这些步骤。

>[!IMPORTANT]
>
>TVSDK不支持单个 `QoSProvider` 以同时使用两者 `itemLoader` 和 `MediaPlayer`. 如果您的应用程序使用Instant On ，则应用程序需要维护两个 `QoS` 实例并管理这两个实例以获取信息。 参见  [即时](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md) 了解更多信息。

1. 创建实例 `MediaPlayerItemLoader`.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
   
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
   
           public void onBufferingBegin() { 
               //Do something 
           } 
   
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       }); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   } 
   ```

   >[!TIP]
   >
   >创建单独的实例 `MediaPlayerItemLoader` 每个资源的。 不要使用一个 `MediaPlayerItemLoader` 实例以加载多个资源。

1. 实施 `ItemLoaderListener` 类以接收来自以下项的通知： `MediaPlayerItemLoader` 实例。

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
           public void onBufferingBegin() { 
               //Do something 
           } 
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       } ); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   }
   ```

   在 `onLoadComplete()` callback，执行以下操作之一：

   * 确保可能影响缓冲的任何操作（例如，选择WebVTT或音频轨道）均已完成，并调用 `prepareBuffer()` 以利用即时打开。
   * 将项目附加到 `MediaPlayer` 实例（通过使用） `replaceCurrentItem()`.
   如果您调用 `prepareBuffer()`，您将在中接收BUFFER_PREPARED事件 `onBufferPrepared` 处理程序完成准备时。

1. 调用 `load` 在 `MediaPlayerItemLoader` 实例并传递要加载的资源，还可以选择传递内容ID和 `MediaPlayerItemConfig` 实例。

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 要从流开头以外的点缓冲，请调用 `prepareBuffer()` 开始缓冲的位置（毫秒）。
1. 使用 `replaceCurrentItem()` 和 `play()` 方法 `MediaPlayer` 从那时起开始播放。
1. 等待空闲状态并调用 `replaceCurrentItem`.
1. 播放项目。

   * 如果项目已加载但未缓冲：

      1. 等待初始化状态。
      1. 调用 `prepareToPlay()`.
      1. 等待PREPARED状态。
      1. 调用 `play()`.
   * 如果项目已缓冲：

      1. 等待缓冲准备事件。
      1. 调用 `play()`.
