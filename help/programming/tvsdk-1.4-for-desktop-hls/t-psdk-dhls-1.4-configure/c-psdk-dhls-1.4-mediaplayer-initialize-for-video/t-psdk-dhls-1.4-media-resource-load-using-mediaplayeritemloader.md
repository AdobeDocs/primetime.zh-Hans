---
description: 解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您希望获取有关特定媒体流的信息而不实例化MediaPlayer实例时，这将很有用。
title: 使用MediaPlayerItemLoader加载媒体资源
exl-id: 08379bd8-1602-4013-a6fb-b1aa6ba539aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 使用MediaPlayerItemLoader加载媒体资源{#load-a-media-resource-using-mediaplayeritemloader}

解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您希望获取有关特定媒体流的信息而不实例化MediaPlayer实例时，这将很有用。

通过 `MediaPlayerItemLoader` 类中，可以交换相应类的媒体资源 `MediaPlayerItem` 而不将视图附加到 `MediaPlayer` 实例计算，这会导致视频解码硬件资源的分配。 获取 `MediaPlayerItem` 实例是异步的。

1. 为以下对象实施事件侦听器 `MediaPlayerItemLoader` 事件：

   * `MediaPlayerItemLoaderEvent.ERROR` 事件

      TVSDK将使用此项来通知您的应用程序发生了错误。 TVSDK提供了一个包含诊断信息的错误属性。

1. 将此实例注册到 `MediaPlayerItemLoader`.
1. 调用 `DefaultMediaPlayerItemLoader.load`，传递 `MediaResource` 对象。

   的URL `MediaResource` 对象必须指向要获取其信息的流。 例如：

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
