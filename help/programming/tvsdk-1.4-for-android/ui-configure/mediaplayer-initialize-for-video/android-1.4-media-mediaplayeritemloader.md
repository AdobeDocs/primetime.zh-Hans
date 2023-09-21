---
description: 解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您希望获取有关特定媒体流的信息而不实例化MediaPlayer实例时，这将很有用。
title: 使用MediaPlayerItemLoader加载媒体资源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 使用MediaPlayerItemLoader加载媒体资源 {#load-a-media-resource-using-mediaplayeritemloader}

解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您希望获取有关特定媒体流的信息而不实例化MediaPlayer实例时，这将很有用。

通过 `MediaPlayerItemLoader` 类中，可以交换相应类的媒体资源 `MediaPlayerItem` 而不将视图附加到 `MediaPlayer` 实例，这会导致视频解码硬件资源的分配。 获取 `MediaPlayerItem` 实例是异步的。

1. 实施 `MediaPlayerItemLoader.LoaderListener` 回调接口。

       此接口定义了两种方法：
   
   * `LoaderListener.onError` 回调函数

     TVSDK将使用此项来通知应用程序发生了错误。 TVSDK提供错误代码作为参数，并提供包含诊断信息的描述字符串。

   * `LoaderListener.onError` 回调函数

     TVSDK将使用此功能通知您的应用程序，请求的信息将以 `MediaPlayerItem` 作为参数传递给回调的实例。

1. 将此实例作为参数传递给 `MediaPlayerItemLoader`.
1. 调用 `MediaPlayerItemLoader.load`，传递 `MediaResource` 对象。

   的URL `MediaResource` 对象必须指向要获取其信息的流。 例如：

   ```java
   // instantiate the listener interface 
   MediaPlayerItemLoader.LoaderListener _itemLoaderListener = 
     new MediaPlayerItemLoader.LoaderListener() { 
       @Override 
       public void onError(MediaErrorCode mediaErrorCode, String description) { 
           // something went wrong - look at the error code and description 
       } 
       @Override 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
           // information is available - look at the data in the "playerItem" object 
       } 
   } 
   
   // instantiate the MediaPlayerItemLoader object (pass the listener as parameter) 
   MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(_itemLoaderListener); 
   
   // create the MediaResource instance and set the URL to point to the actual media stream 
   MediaResource mediaResource =  
     MediaResource.createFromUrl("https://test.com/test_media.m3u8", null); 
   
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```
