---
description: 并行下载视频和音频（而不是串行下载）可减少启动延迟。
title: 并行下载
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 并行下载{#parallel-downloads}

并行下载视频和音频（而不是串行下载）可减少启动延迟。

并行下载允许播放视频点播(VOD)文件，优化来自服务器的可用带宽使用，降低在运行不足情况下进入缓冲区的可能性，并最小化下载和回放之间的延迟。

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

如果没有并行下载，TVSDK会发出对视频段的请求，在加载视频段后，它会请求一个或两个音频段。 通过并行下载，音频和视频段可以同时下载，而不是按顺序下载。 此外，由于每个区段有两个连接和两个HTTP请求并行，因此数据可以更快地到达屏幕。

>[!NOTE]
>
>此功能仅适用于将音频和视频编码为不同文件（未混合内容）的内容，不适用于始终混合的MP4内容。 HLS内容通常是未混合的，尤其是具有替代音频的内容。

<!-- 

See comment above (DASH use case removed).
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

HTTP连接可能在以下阶段遇到延迟：

* 在与服务器建立TCP/IP连接时

   虽然客户端和服务器已同意进行通信，但尚未进行HTTP通信。 这种类型的延迟取决于客户端和服务器之间的基础架构。 此过程要求在客户端和服务器之间找到一条通过互联网的路径，并确保路由上的所有设备（如路由器和防火墙）都同意数据传输。
* 通过TCP/IP连接发送段或清单的HTTP请求时。

   服务器接收请求，处理请求，并将数据发送回客户端的开始。 延迟的程度取决于服务器上软件的负载和复杂性，在某种程度上取决于客户端发送请求时的上载连接速度。

