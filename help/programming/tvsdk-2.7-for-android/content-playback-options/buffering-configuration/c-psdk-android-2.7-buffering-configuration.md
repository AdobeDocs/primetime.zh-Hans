---
description: 为了提供更流畅的观看体验，TVSDK有时会缓冲视频流。 您可以配置播放器的缓冲方式。
title: 缓冲
exl-id: f4df3084-376e-421c-aaa5-83de2815dabe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# 概述 {#buffering-overview}

为了提供更流畅的观看体验，TVSDK有时会缓冲视频流。 您可以配置播放器的缓冲方式。

TVSDK定义的播放缓冲区长度至少为30秒，媒体开始播放前的初始缓冲时间至少为2秒。 在应用程序调用之后 `play`，但在播放开始之前，TVSDK会缓冲媒体直到初始时间，以便在媒体实际开始播放时提供顺利的开始。

您可以通过定义新的缓冲策略来更改缓冲时间，还可以使用立即打开来更改初始缓冲发生时的缓冲时间。

## 缓冲时间策略 {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

根据您的环境（包括设备、操作系统或网络条件），您可以为播放器设置不同的缓冲策略，例如更改初始缓冲和持续播放缓冲的最小持续时间。

在您调用之后 `play`，媒体播放器开始缓冲视频。 当媒体播放器缓冲了由初始缓冲时间指定的视频量时，开始播放。 此过程可缩短启动时间，因为播放器在开始播放之前不会等待整个播放缓冲区填充。 相反，在缓冲了几个初始秒数后，开始播放。

在渲染视频时，TVSDK将继续缓冲新片段，直到缓冲了播放缓冲时间指定的量为止。 如果当前缓冲区长度低于播放缓冲区时间，播放器将下载其他片段。 一旦当前缓冲区长度超过播放缓冲区时间几秒钟，TVSDK将停止下载片段。

>[!TIP]
>
>如果初始缓冲值很高，它可能会给用户较长的初始缓冲时间，然后再开始。 这样可以提供更长时间的流畅播放；但是，如果网络条件较差，初始播放可能会延迟。

如果通过呼叫启用即时打开 `prepareBuffer`时，初始缓冲此时开始，而不是等待 `play`.

## 设置缓冲时间 {#section_05CDD927869D47EBA1D2069B1416B2E4}

此 `MediaPlayer` 提供了设置和获取初始缓冲时间和播放缓冲时间的方法。

>[!TIP]
>
>如果在开始播放之前未设置缓冲控制参数，则媒体播放器默认为2秒作为初始缓冲时间，30秒作为持续播放缓冲时间。

1. 设置 `BufferControlParameters` 对象，封装了初始缓冲时间和播放缓冲时间控制参数。

   此类提供以下工厂方法：

   * 要将初始缓冲时间设置为等于播放缓冲时间，请执行以下操作：

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * 要设置初始缓冲时间和播放缓冲时间，请执行以下操作：

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   如果参数无效，则这些方法会引发 `MediaPlayerException` 带有错误代码 `PSDKErrorCode.INVALID_ARGUMENT`，例如当满足以下条件时：

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

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

例如，要将初始缓冲设置为5秒，将播放缓冲时间设置为30秒，请执行以下操作：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
