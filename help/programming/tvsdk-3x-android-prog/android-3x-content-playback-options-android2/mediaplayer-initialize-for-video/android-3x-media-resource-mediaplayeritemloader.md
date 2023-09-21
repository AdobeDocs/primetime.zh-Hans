---
description: 使用MediaPlayerItemLoader有助于获取有关媒体流的信息，而无需实例化MediaPlayer实例。 在预缓冲流中尤其有用，因为这样可以毫不延迟地开始播放。
title: 使用MediaPlayerItemLoader加载媒体资源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# 使用MediaPlayerItemLoader加载媒体资源 {#load-a-media-resource-using-mediaplayeritemloader}

使用MediaPlayerItemLoader有助于获取有关媒体流的信息，而无需实例化MediaPlayer实例。 在预缓冲流中尤其有用，因为这样可以毫不延迟地开始播放。

此 `MediaPlayerItemLoader` 类帮助您交换当前介质的媒体资源 `MediaPlayerItem` 而不将视图附加到 `MediaPlayer` 实例，用于分配视频解码硬件资源。 对于受DRM保护的内容，还需要执行其他步骤，但本手册未介绍这些步骤。

>[!IMPORTANT]
>
>TVSDK不支持单个 `QoSProvider` 以同时使用两者 `itemLoader` 和 `MediaPlayer`. 如果您的应用程序使用Instant On ，则应用程序需要维护两个 `QoS` 实例并管理这两个实例以获取信息。 请参阅 [即时](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) 以了解更多信息。

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
   >创建单独的实例 `MediaPlayerItemLoader` 每个资源对应的URL。 不要使用一个 `MediaPlayerItemLoader` 实例以加载多个资源。

1. 实施 `ItemLoaderListener` 类以接收来自的通知 `MediaPlayerItemLoader` 实例。

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

   * 确保任何可能影响缓冲的内容（例如，选择WebVTT或音频轨道）均已完成并调用 `prepareBuffer()` 以利用即时打开。
   * 将项目附加到 `MediaPlayer` 使用实例 `replaceCurrentItem()`.

   如果您致电 `prepareBuffer()`，您将在中接收BUFFER_PREPARED事件 `onBufferPrepared` 处理程序完成准备时。
1. 调用 `load` 在 `MediaPlayerItemLoader` 实例并传递要加载的资源，还可以选择传递内容ID和 `MediaPlayerItemConfig` 实例。

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 要从流开头以外的点缓冲，请调用 `prepareBuffer()` 开始缓冲的位置（以毫秒为单位）。
1. 使用 `replaceCurrentItem()` 和 `play()` 方法 `MediaPlayer` 从那点开始播放。
1. 等待空闲状态并调用 `replaceCurrentItem`.
1. 播放项目。

   * 如果加载了项目但未缓冲：

      1. 等待初始化的状态。
      1. 调用 `prepareToPlay()`.
      1. 等待“已准备”状态。
      1. 调用 `play()`.

   * 如果项目已缓冲：

      1. 等待缓冲准备事件。
      1. 调用 `play()`.
