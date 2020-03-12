---
description: 并行下载视频和音频（而不是串行下载）可减少启动延迟。
seo-description: 并行下载视频和音频（而不是串行下载）可减少启动延迟。
seo-title: 并行下载
title: 并行下载
uuid: 11d37a39-391d-4127-9aa7-c94eb8a6a6a8
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 并行下载 {#parallel-downloads}

并行下载视频和音频（而不是串行下载）可减少启动延迟。

并行下载允许播放视频点播(VOD)文件，优化来自服务器的可用带宽使用，降低进入缓冲区运行不足的可能性，并最小化下载和回放之间的延迟。

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

如果没有并行下载，TVSDK会发出视频段的请求，在加载视频段后，它会请求一个或两个音频段。 通过并行下载，音频和视频段是同时下载的，而不是按顺序下载的。 此外，由于每个区段有两个连接和两个HTTP请求并行，因此数据到达屏幕的速度会更快。

>[!NOTE]
>
>此功能仅适用于将音频和视频编码为不同文件（未混合内容）的内容，而不适用于MP4内容（始终为混合内容）。 HLS内容通常会取消混合，尤其是使用替代音频。

<!-- 

See comment above (DASH use case removed).
<note type="restriction">
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
</note>

 -->

HTTP连接可能在以下阶段遇到延迟：

* 在与服务器建立TCP/IP连接时

   虽然客户端和服务器已同意进行通信，但尚未进行HTTP通信。 这种类型的延迟取决于客户端和服务器之间的基础架构。 此过程需要在客户端和服务器之间查找通过Internet的路径，并确保路由器和防火墙等所有设备都同意数据传输。
* 通过TCP/IP连接发送段或清单的HTTP请求时。

   服务器接收请求，处理请求，然后开始将数据发送回客户端。 延迟程度取决于服务器上的负载和软件的复杂性，在某种程度上取决于客户端发送请求时的上传连接速度。