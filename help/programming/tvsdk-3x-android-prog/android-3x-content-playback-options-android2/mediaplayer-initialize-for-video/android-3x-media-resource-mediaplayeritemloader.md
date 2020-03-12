---
description: 使用MediaPlayerItemLoader可以帮助您获得有关媒体流的信息，而无需实例化MediaPlayer实例。 这在预缓冲流中尤其有用，这样可以无延迟地开始播放。
seo-description: 使用MediaPlayerItemLoader可以帮助您获得有关媒体流的信息，而无需实例化MediaPlayer实例。 这在预缓冲流中尤其有用，这样可以无延迟地开始播放。
seo-title: 使用MediaPlayerItemLoader加载媒体资源
title: 使用MediaPlayerItemLoader加载媒体资源
uuid: 504063af-1dd4-4268-88e7-ad5a247fdff7
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc

---


# 使用MediaPlayerItemLoader加载媒体资源 {#load-a-media-resource-using-mediaplayeritemloader}

使用MediaPlayerItemLoader可以帮助您获得有关媒体流的信息，而无需实例化MediaPlayer实例。 这在预缓冲流中尤其有用，这样可以无延迟地开始播放。

该 `MediaPlayerItemLoader` 类帮助您为当前媒体资源交换媒体资源，而 `MediaPlayerItem` 不将视图附加到实例，该实例将分 `MediaPlayer` 配视频解码硬件资源。 对于受DRM保护的内容，需要执行其他步骤，但本手册不描述这些步骤。

>[!IMPORTANT]
>
>TVSDK不支持同时使用 `QoSProvider` 和的单个 `itemLoader` 软件 `MediaPlayer`。 如果应用程序使用“即时启动”，则应用程序需要维护两个实 `QoS` 例并管理两个实例以获取相关信息。 请参 [阅即时启动](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) ，以了解更多信息。

1. 创建实例 `MediaPlayerItemLoader`。

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
   >为每个资源创建单 `MediaPlayerItemLoader` 独的实例。 请勿使用一个实 `MediaPlayerItemLoader` 例加载多个资源。

1. 实现类 `ItemLoaderListener` 以接收来自实例的 `MediaPlayerItemLoader` 通知。

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

   在回调 `onLoadComplete()` 中，执行下列操作之一：

   * 确保任何可能影响缓冲的内容（例如，选择WebVTT或音轨）都已完成并调用以 `prepareBuffer()` 便利用即时开启。
   * 使用将项目附加 `MediaPlayer` 到实例 `replaceCurrentItem()`。
   如果调用 `prepareBuffer()`，准备完成时，您将在处理函数中 `onBufferPrepared` 收到BUFFER_PREPARED事件。
1. 调 `load` 用实 `MediaPlayerItemLoader` 例并传递要加载的资源，可选地传递内容ID和实 `MediaPlayerItemConfig` 例。

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 要从流开头以外的点进行缓冲，请 `prepareBuffer()` 调用要开始缓冲的位置（以毫秒为单位）。
1. 使用 `replaceCurrentItem()` 和 `play()` 方法 `MediaPlayer` 从该点开始播放。
1. 等待空闲状态并拨叫 `replaceCurrentItem`。
1. 播放项目。

   * 如果已加载但未缓冲项：

      1. 等待初始化状态。
      1. 打 `prepareToPlay()`电话。
      1. 等待PREPARED状态。
      1. 打 `play()`电话。
   * 如果项已缓冲：

      1. 等待缓冲区预准备事件。
      1. 打 `play()`电话。