---
description: MediaPlayer提供设置和获取初始缓冲时间和回放缓冲时间的方法。
seo-description: MediaPlayer提供设置和获取初始缓冲时间和回放缓冲时间的方法。
seo-title: 设置缓冲时间
title: 设置缓冲时间
uuid: 25142b01-5381-49c9-b89a-24c858faaf13
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 设置缓冲时间{#set-buffering-times}

MediaPlayer提供设置和获取初始缓冲时间和回放缓冲时间的方法。

>[!TIP]
>
>如果在开始播放之前未设置缓冲区控制参数，媒体播放器将初始缓冲区默认为2秒，当前播放缓冲区时间默认为30秒。

1. 设置`BufferControlParameters`对象，该对象封装初始缓冲时间和播放缓冲时间控制参数：

       此类提供以下工厂方法：
   
   * 要将初始缓冲时间设置为等于播放缓冲时间：

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * 要同时设置初始和播放缓冲时间：

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      如果参数无效，则这些方法将抛出`IllegalArgumentException`，例如：

   * 初始缓冲时间小于零。
   * 初始缓冲时间大于缓冲时间。

1. 要设置缓冲区参数值，请使用以下`MediaPlayer`方法：

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. 要获取当前缓冲区参数值，请使用以下`MediaPlayer`方法：

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，要将初始缓冲区设置为2秒，将播放缓冲区时间设置为30秒：

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

`psdkdemo`演示此功能；使用应用程序的设置设置缓冲区值。
