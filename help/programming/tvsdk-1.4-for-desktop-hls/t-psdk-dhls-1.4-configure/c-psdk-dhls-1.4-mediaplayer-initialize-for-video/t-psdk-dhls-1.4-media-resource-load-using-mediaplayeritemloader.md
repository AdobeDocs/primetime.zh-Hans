---
description: 解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您要获取有关特定媒体流的信息而不实例化MediaPlayer实例时，这非常有用。
seo-description: 解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您要获取有关特定媒体流的信息而不实例化MediaPlayer实例时，这非常有用。
seo-title: 使用MediaPlayerItemLoader加载媒体资源
title: 使用MediaPlayerItemLoader加载媒体资源
uuid: a7ec8f58-7357-4757-a402-e879dd6caec8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 使用MediaPlayerItemLoader加载媒体资源{#load-a-media-resource-using-mediaplayeritemloader}

解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您要获取有关特定媒体流的信息而不实例化MediaPlayer实例时，这非常有用。

通过该 `MediaPlayerItemLoader` 类，您可以交换相应的媒体资源，而不将视图附加到实例 `MediaPlayerItem``MediaPlayer` ，这将导致视频解码硬件资源的分配。 获取实例的过 `MediaPlayerItem` 程是异步的。

1. 为以下事件实施事件监 `MediaPlayerItemLoader` 听器：

   * `MediaPlayerItemLoaderEvent.ERROR` event

      TVSDK使用它通知您的应用程序发生了错误。 TVSDK提供包含诊断信息的错误属性。

1. 将此实例注册到 `MediaPlayerItemLoader`。
1. 调 `DefaultMediaPlayerItemLoader.load`用，传递对象的实 `MediaResource` 例。

   对象的URL `MediaResource` 必须指向要获取其信息的流。 例如：

   ```
   private function onLoadError(event:MediaPlayerItemLoaderEvent):void { 
       // something went wrong - look at the error code and description 
       // contained within the event.error 
   } 
   private function onLoadCompleted(event:MediaPlayerItemLoaderEvent):void { 
       // information is available - look at the data in the "event.item" object 
   } 
   // instantiate the MediaPlayerItemLoader object and register event listeners 
   var itemLoader:MediaPlayerItemLoader = new DefaultMediaPlayerItemLoader(); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.ERROR, onLoadError); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.COMPLETED, onLoadCompleted); 
   // create the MediaResource instance and set the URL to point to the actual media stream 
   var mediaResource:MediaResource = 
     MediaResource.createFromURL("https://example.com/media/test_media.m3u8", null); 
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```

