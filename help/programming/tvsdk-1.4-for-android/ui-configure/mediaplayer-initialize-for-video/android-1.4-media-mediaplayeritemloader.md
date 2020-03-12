---
description: 解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您要获取有关特定媒体流的信息而不实例化MediaPlayer实例时，这非常有用。
seo-description: 解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您要获取有关特定媒体流的信息而不实例化MediaPlayer实例时，这非常有用。
seo-title: 使用MediaPlayerItemLoader加载媒体资源
title: 使用MediaPlayerItemLoader加载媒体资源
uuid: b2311ddc-f059-4775-8553-fc354ec2636b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 使用MediaPlayerItemLoader加载媒体资源 {#load-a-media-resource-using-mediaplayeritemloader}

解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您要获取有关特定媒体流的信息而不实例化MediaPlayer实例时，这非常有用。

通过该 `MediaPlayerItemLoader` 类，您可以交换相应的媒体资源，而不将视图附加到实例 `MediaPlayerItem``MediaPlayer` ，这将导致视频解码硬件资源的分配。 获取实例的过 `MediaPlayerItem` 程是异步的。

1. 实现回 `MediaPlayerItemLoader.LoaderListener` 调接口。

       此接口定义两种方法：
   
   * `LoaderListener.onError` 回调函数

      TVSDK使用它通知您的应用程序发生了错误。 TVSDK提供错误代码作为参数和包含诊断信息的描述字符串。

   * `LoaderListener.onError` 回调函数

      TVSDK使用它通知您的应用程序，请求的信息以实例的形式可用，该实例作为参数传递给回调。 `MediaPlayerItem`

1. 将此实例作为参数传递给TVSDK的构造函数，以将其注册到TVSDK `MediaPlayerItemLoader`。
1. 调 `MediaPlayerItemLoader.load`用，传递对象的实 `MediaResource` 例。

   对象的URL `MediaResource` 必须指向要获取其信息的流。 例如：

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

