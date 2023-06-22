---
description: 并行下载视频和音频而不是串联下载可减少启动延迟。
title: 并行下载
exl-id: 6c93154b-8de4-448b-bc33-776fcc1f6243
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 并行下载 {#parallel-downloads}

并行下载视频和音频而不是串联下载可减少启动延迟。

并行下载允许播放视频点播(VOD)文件，优化来自服务器的可用带宽使用，降低进入缓冲区不足的概率，并最大限度地减少下载和播放之间的延迟。

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

如果没有并行下载，TVSDK会向视频区段发出请求，并且在加载视频区段后，它会请求一个或两个音频区段。 通过并行下载，音频和视频区段是同时下载的，而不是按顺序下载。 此外，由于每个区段有两个连接和两个HTTP请求并行，因此数据到达屏幕的速度更快。

>[!NOTE]
>
>此功能仅适用于音频和视频被编码为不同文件（未混合的内容）的内容，而不适用于MP4内容，MP4内容始终混合在一起。 HLS内容通常会取消混音，尤其是使用替代音频时。

<!-- 

See comment above (DASH use case removed).
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

HTTP连接可能在以下阶段遇到延迟：

* 建立与服务器的TCP/IP连接时

   尽管客户端和服务器同意通信，但尚未发生HTTP通信。 这种延迟类型取决于客户端和服务器之间的基础架构。 此过程需要找到客户端和服务器之间的互联网路径，并确保路由上的所有设备（如路由器和防火墙）都同意数据传输。
* 通过TCP/IP连接发送区段或清单的HTTP请求时。

   服务器接收并处理请求，然后开始将数据发送回客户端。 延迟的程度取决于服务器上的软件的负载和复杂性，并且在一定程度上取决于客户端发送请求时的上传连接速度。
