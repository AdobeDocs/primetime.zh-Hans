---
description: 为了提供更流畅的观看体验，TVSDK有时会缓冲视频流。 您可以配置播放器的缓冲方式。
title: 设置缓冲时间
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 缓冲 {#buffering}

为了提供更流畅的观看体验，TVSDK有时会缓冲视频流。 您可以配置播放器的缓冲方式。

TVSDK定义的播放缓冲时间长度至少为30秒，其中在媒体开始播放之前的初始缓冲时间至少为2秒。 在应用程序调用之后 `play` 但在播放开始之前，TVSDK会缓冲媒体，直到初始时间为止，以便在媒体实际开始播放时提供顺利的开始。

您可以通过定义新的缓冲策略来更改缓冲时间，还可以使用即时启动在初始缓冲发生时进行更改。

## 设置缓冲时间 {#set-buffering-times}

此 `MediaPlayer` 提供了设置和获取初始缓冲时间和播放缓冲时间的方法。

>[!TIP]
>
>如果在开始播放之前未设置缓冲控制参数，则媒体播放器将默认使用2秒作为初始缓冲时间，30秒作为持续播放缓冲时间。

1. 设置 `BufferControlParameters` 对象，封装了初始缓冲时间和播放缓冲时间控制参数：

       此类提供两种工厂方法：
   
   * 要将初始缓冲时间设置为等于播放缓冲时间，请执行以下操作：

     ```java
     public static BufferControlParameters createSimple( 
         long bufferTime)
     ```

   * 要设置初始缓冲时间和播放缓冲时间，请执行以下操作：

     ```java
     public static BufferControlParameters createDual( 
         long initialBuffer,   
         long bufferTime)
     ```

     这些方法会引发 `IllegalArgumentException` 如果参数无效，例如：

   * 初始缓冲时间小于零。
   * 初始缓冲时间大于缓冲时间。

1. 要设置缓冲区参数值，请使用此 `MediaPlayer` 方法：

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. 要获取当前缓冲区参数值，请使用此 `MediaPlayer` 方法：

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   如果AVE无法设置指定的值，媒体播放器将输入 `ERROR` 带有错误代码的状态 `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，将初始缓冲设置为2秒，将播放缓冲时间设置为30秒：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

Primetime参考实施演示了此功能；使用应用程序的设置设置设置缓冲区值。
