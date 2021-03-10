---
description: 为了提供更流畅的查看体验，TVSDK有时会缓冲视频流。 您可以配置播放器缓冲的方式。
title: 设置缓冲时间
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# 缓冲{#buffering}

为了提供更流畅的查看体验，TVSDK有时会缓冲视频流。 您可以配置播放器缓冲的方式。

TVSDK定义至少30秒的播放缓冲长度和至少2秒的初始缓冲时间，在播放媒体开始之前，该时间内的初始缓冲时间。 在应用程序调用`play`但在播放开始之前，TVSDK会将媒体缓冲到初始时间，以在实际开始播放时提供平滑开始。

您可以通过定义新的缓冲策略来更改缓冲时间，也可以通过使用即时启动来更改初始缓冲的时间。

## 设置缓冲时间{#set-buffering-times}

`MediaPlayer`提供了设置和获取初始缓冲时间和回放缓冲时间的方法。

>[!TIP]
>
>如果在开始播放之前未设置缓冲区控制参数，则媒体播放器默认初始缓冲区为2秒，当前播放缓冲区时间为30秒。

1. 设置`BufferControlParameters`对象，该对象封装初始缓冲时间和播放缓冲时间控制参数：

       此类提供两种工厂方法：
   
   * 要将初始缓冲时间设置为等于播放缓冲时间：

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

      如果参数无效，则这些方法将引发`IllegalArgumentException`，例如：

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

   如果AVE无法设置指定的值，媒体播放器将进入`ERROR`状态，错误代码为`SET_BUFFER_PARAMETERS_ERROR`。

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，要将初始缓冲区设置为2秒，将播放缓冲区时间设置为30秒：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

Primetime参考实施演示了此功能；使用应用程序的设置设置缓冲区值。