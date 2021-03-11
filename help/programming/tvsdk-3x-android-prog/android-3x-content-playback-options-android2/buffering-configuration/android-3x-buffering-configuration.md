---
description: 为了提供更流畅的查看体验，TVSDK有时会缓冲视频流。 您可以配置播放器缓冲的方式。
title: 缓冲
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---


# 概述{#buffering-overview}

为了提供更流畅的查看体验，TVSDK有时会缓冲视频流。 您可以配置播放器缓冲的方式。

TVSDK定义至少30秒的播放缓冲长度和至少2秒的媒体开始播放前的初始缓冲时间。 在应用程序调用`play`后，但在播放开始之前，TVSDK会将媒体缓冲到初始时间，以在实际播放开始时提供平滑开始。

您可以通过定义新的缓冲策略来更改缓冲时间，也可以通过使用“即时开”来更改初始缓冲的时间。

## 缓冲时间策略{#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

根据您的环境（包括设备、操作系统或网络条件），可以为播放器设置不同的缓冲策略，如更改初始缓冲和当前播放缓冲的最短持续时间。

调用`play`后，媒体播放器开始缓冲视频。 当媒体播放器缓冲了初始缓冲时间指定的视频量时，播放开始。 此过程会缩短开始启动时间，因为播放器不会等待整个播放缓冲区填充，然后开始播放。 相反，在缓冲几秒后，播放开始。

在渲染视频时，TVSDK继续缓冲新片段，直到它缓冲了播放缓冲时间指定的量。 如果当前缓冲区长度低于播放缓冲区时间，播放器将下载其他片段。 当当前缓冲区长度超过播放缓冲时间几秒后，TVSDK将停止下载片段。

>[!TIP]
>
>如果初始缓冲区值较高，则可能会在开始前为用户提供较长的初始缓冲时间。 这可能会让播放更加流畅；但是，如果网络条件较差，初始播放可能会延迟。

如果通过调用`prepareBuffer`启用即时，则初始缓冲将从该刻开始，而不是等待`play`。

## 设置缓冲时间{#section_05CDD927869D47EBA1D2069B1416B2E4}

`MediaPlayer`提供了设置和获取初始缓冲时间和回放缓冲时间的方法。

>[!TIP]
>
>如果在开始播放之前未设置缓冲区控制参数，则媒体播放器默认初始缓冲区为2秒，当前播放缓冲区时间为30秒。

1. 设置`BufferControlParameters`对象，该对象封装初始缓冲时间和回放缓冲时间控制参数。

   此类提供以下工厂方法：

   * 要将初始缓冲时间设置为等于播放缓冲时间：

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * 设置初始和播放缓冲时间：

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   如果参数无效，则这些方法将引发错误代码为`PSDKErrorCode.INVALID_ARGUMENT`的`MediaPlayerException`，例如当满足以下条件时：

   * 初始缓冲时间小于零。
   * 初始缓冲时间大于缓冲时间。


1. 要设置缓冲区参数值，请使用以下`MediaPlayer`方法：

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. 要获取当前缓冲区参数值，请使用以下`MediaPlayer`方法：

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

例如，要将初始缓冲区设置为5秒，将播放缓冲区时间设置为30秒：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
