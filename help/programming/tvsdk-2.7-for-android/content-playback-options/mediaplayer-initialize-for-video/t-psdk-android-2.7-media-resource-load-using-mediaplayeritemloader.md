---
description: 使用MediaPlayerItemLoader可以帮助您获取有关媒体流的信息，而无需实例化MediaPlayer实例。 这在预缓冲流中特别有用，这样可以无延迟地开始播放。
title: 使用MediaPlayerItemLoader加载媒体资源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# 使用MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}加载媒体资源

使用MediaPlayerItemLoader可以帮助您获取有关媒体流的信息，而无需实例化MediaPlayer实例。 这在预缓冲流中特别有用，这样可以无延迟地开始播放。

`MediaPlayerItemLoader`类帮助您交换当前`MediaPlayerItem`的媒体资源，而不将视图附加到将分配视频解码硬件资源的`MediaPlayer`实例。 对于受DRM保护的内容，需要执行其他步骤，但本手册并未说明这些步骤。

>[!IMPORTANT]
>
>TVSDK不支持单个`QoSProvider`以同时与`itemLoader`和`MediaPlayer`一起使用。 如果应用程序使用“即时启动”，则应用程序需要维护两个`QoS`实例并管理两个实例以获取相关信息。 有关详细信息，请参阅[instant-on](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md)。

1. 创建`MediaPlayerItemLoader`的实例。

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
   >为每个资源创建一个单独的`MediaPlayerItemLoader`实例。 请勿使用一个`MediaPlayerItemLoader`实例加载多个资源。

1. 实现`ItemLoaderListener`类以接收来自`MediaPlayerItemLoader`实例的通知。

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

   在`onLoadComplete()`回调中，执行以下操作之一：

   * 确保任何可能影响缓冲的内容（例如，选择WebVTT或音轨）都已完成，并调用`prepareBuffer()`以便立即打开。
   * 使用`replaceCurrentItem()`将项目连接到`MediaPlayer`实例。

   如果调用`prepareBuffer()`，则在准备完成后，您将在`onBufferPrepared`处理函数中收到BUFFER_PREPARED事件。

1. 调用`MediaPlayerItemLoader`实例上的`load`并传递要加载的资源、内容ID和`MediaPlayerItemConfig`实例（可选）。

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. 要从流开头以外的点进行缓冲，请使用开始缓冲的位置（以毫秒为单位）调用`prepareBuffer()`。
1. 使用`MediaPlayer`的`replaceCurrentItem()`和`play()`方法，从该点开始播放开始。
1. 等待空闲状态并调用`replaceCurrentItem`。
1. 播放项目。

   * 如果已加载但未缓冲该项：

      1. 等待初始化状态。
      1. 调用`prepareToPlay()`。
      1. 等待PREPARED状态。
      1. 调用`play()`。
   * 如果缓冲了项：

      1. 等待缓冲区准备事件。
      1. 调用`play()`。