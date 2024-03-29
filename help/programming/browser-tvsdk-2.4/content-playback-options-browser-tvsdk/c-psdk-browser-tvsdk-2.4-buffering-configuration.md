---
description: 为了提供更流畅的观看体验，浏览器TVSDK有时会缓冲视频流。 您可以配置播放器的缓冲方式。
title: 缓冲
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# 缓冲{#buffering}

为了提供更流畅的观看体验，浏览器TVSDK有时会缓冲视频流。 您可以配置播放器的缓冲方式。

浏览器TVSDK定义的播放缓冲时间长度至少为30秒，其中在媒体开始播放之前的初始缓冲时间至少为2秒。 在应用程序调用之后 `play` 但在播放开始之前，浏览器TVSDK会缓冲媒体，直至初始时间为止，以便在媒体实际开始播放时提供顺利的开始。

## 设置缓冲时间 {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

MediaPlayer提供了一些方法来设置和获取初始缓冲时间和播放缓冲时间。

>[!TIP]
>
>如果在开始播放之前未设置缓冲控制参数，则媒体播放器将默认使用2秒作为初始缓冲时间，30秒作为持续播放缓冲时间。

* 若要使用缓冲区参数，请使用 `bufferControlParameters` 属性。

  例如，将初始缓冲设置为2秒，将播放缓冲时间设置为30秒：

  ```js
  var params = new AdobePSDK.BufferControlParameters(2000, 30000);
  ```

## 缓冲时间策略 {#section_7EF2947931654CCC8DAB9172391FA4EB}

根据环境（包括设备、操作系统或网络条件）的不同，可以为播放器设置不同的缓冲策略，例如更改初始缓冲和持续播放缓冲的最短持续时间。

在您致电之后 `play`，媒体播放器会开始缓冲视频。 当媒体播放器缓冲了由初始缓冲时间指定的视频量时，将开始播放。 此过程可缩短启动时间，因为播放器在开始播放之前不会等待整个播放缓冲区填充完毕。 相反，在缓冲了几个初始秒数后，开始播放。

在渲染视频时，浏览器TVSDK将继续缓冲新片段，直到缓冲了播放缓冲时间指定的量为止。 如果当前缓冲区长度低于播放缓冲时间，播放器将下载其他片段。 一旦当前缓冲区长度超过播放缓冲区时间几秒钟，浏览器TVSDK将停止下载片段。

>[!TIP]
>
>如果初始缓冲值很高，它可能会给用户较长的初始缓冲时间，然后才能开始。 这样可以提供更长时间的流畅播放；但是，如果网络条件较差，初始播放可能会延迟。
