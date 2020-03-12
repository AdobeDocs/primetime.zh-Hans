---
description: 为了提供更流畅的查看体验，TVSDK有时会缓冲视频流。 您可以配置播放器缓冲的方式。
seo-description: 为了提供更流畅的查看体验，TVSDK有时会缓冲视频流。 您可以配置播放器缓冲的方式。
seo-title: 设置缓冲时间
title: 设置缓冲时间
uuid: 5a3945a4-1935-4797-b19d-84989850a487
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 缓冲 {#buffering}

为了提供更流畅的查看体验，TVSDK有时会缓冲视频流。 您可以配置播放器缓冲的方式。

TVSDK定义至少30秒的播放缓冲长度，以及在媒体开始播放之前至少2秒的初始缓冲时间。 在应用程序调 `play` 用后但在播放开始之前，TVSDK会将媒体缓冲到初始时间，以在实际开始播放时顺利开始。

您可以通过定义新的缓冲策略来更改缓冲时间，也可以使用即时启动来更改初始缓冲的时间。

## 设置缓冲时间 {#set-buffering-times}

提供 `MediaPlayer` 了设置和获取初始缓冲时间和回放缓冲时间的方法。

>[!TIP]
>
>如果在开始播放之前未设置缓冲区控制参数，则媒体播放器默认为初始缓冲区的2秒，当前播放缓冲区的30秒。

1. 设置对象， `BufferControlParameters` 该对象封装初始缓冲时间和回放缓冲时间控制参数：

       此类提供两种工厂方法：
   
   * 将初始缓冲时间设置为等于播放缓冲时间：

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * 设置初始和播放缓冲时间：

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      如果参数 `IllegalArgumentException` 无效，则这些方法将引发以下问题：

   * 初始缓冲时间小于零。
   * 初始缓冲时间大于缓冲时间。

1. 要设置缓冲区参数值，请使用此 `MediaPlayer` 方法：

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. 要获取当前缓冲区参数值，请使用以下 `MediaPlayer` 方法：

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   如果AVE无法设置指定的值，则媒体播放器将进 `ERROR` 入包含错误代码的状态 `SET_BUFFER_PARAMETERS_ERROR`。

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，要将初始缓冲区设置为2秒，将播放缓冲区时间设置为30秒：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

Primetime参考实施演示了此功能；使用应用程序的设置设置缓冲区值。