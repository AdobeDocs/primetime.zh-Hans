---
description: MediaPlayer提供了一些方法来设置和获取初始缓冲时间和播放缓冲时间。
title: 设置缓冲时间
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# 设置缓冲时间{#set-buffering-times}

MediaPlayer提供了一些方法来设置和获取初始缓冲时间和播放缓冲时间。

>[!TIP]
>
>如果在开始播放之前未设置缓冲控制参数，则媒体播放器将默认使用2秒作为初始缓冲时间，30秒作为持续播放缓冲时间。

1. 设置 `BufferControlParameters` 对象，封装了初始缓冲时间和播放缓冲时间控制参数：

       此类提供了以下工厂方法：
   
   * 要将初始缓冲时间设置为等于播放缓冲时间，请执行以下操作：

     ```
     createSimple(bufferTime:uint):BufferControlParameters
     ```

   * 要设置初始缓冲时间和播放缓冲时间，请执行以下操作：

     ```
     createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
     ```

     这些方法会引发 `IllegalArgumentException` 如果参数无效，例如：

   * 初始缓冲时间小于零。
   * 初始缓冲时间大于缓冲时间。

1. 要设置缓冲区参数值，请使用此 `MediaPlayer` 方法：

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. 要获取当前缓冲区参数值，请使用此 `MediaPlayer` 方法：

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，将初始缓冲设置为2秒，将播放缓冲时间设置为30秒：

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

此 `psdkdemo` 演示此功能；使用应用程序的设置设置设置缓冲区值。
