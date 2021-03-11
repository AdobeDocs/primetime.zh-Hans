---
description: 解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您想要获取有关特定媒体流的信息而不实例化MediaPlayer实例时，此功能非常有用。
title: 使用MediaPlayerItemLoader加载媒体资源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# 使用MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}加载媒体资源

解析媒体资源的另一种方法是使用MediaPlayerItemLoader。 当您想要获取有关特定媒体流的信息而不实例化MediaPlayer实例时，此功能非常有用。

通过`MediaPlayerItemLoader`类，您可以交换相应`MediaPlayerItem`的媒体资源，而不将视图附加到`MediaPlayer`实例，这会导致分配视频解码硬件资源。 获取`MediaPlayerItem`实例的过程是异步的。

1. 实现`MediaPlayerItemLoader.LoaderListener`回调接口。

       此接口定义两种方法：
   
   * `LoaderListener.onError` 回调函数

      TVSDK使用它通知您的应用程序发生错误。 TVSDK提供错误代码作为参数和包含诊断信息的描述字符串。

   * `LoaderListener.onError` 回调函数

      TVSDK使用它通知您的应用程序，请求的信息以`MediaPlayerItem`实例的形式可用，该实例作为参数传递给回调。

1. 通过将此实例作为参数传递给`MediaPlayerItemLoader`的构造函数，将其注册到TVSDK。
1. 调用`MediaPlayerItemLoader.load`，传递`MediaResource`对象的实例。

   `MediaResource`对象的URL必须指向要获取其信息的流。 例如：

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

