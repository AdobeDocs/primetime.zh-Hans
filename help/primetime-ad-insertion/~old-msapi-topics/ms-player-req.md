---
description: 所有视频播放器都必须提供清单服务器所依赖的功能，才能插入广告并启用广告跟踪。
title: 视频播放器要求
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 视频播放器要求 {#video-player-requirements}

所有视频播放器都必须提供清单服务器所依赖的功能，才能插入广告并启用广告跟踪。

要使用Primetime广告插入API，视频播放器必须满足以下条件：

* 可以在播放内容时跟踪播放头位置。
* 可以在指定的时间请求跟踪URL。
* 在支持HLS v3或更高版本的设备平台上运行，包括：

   * 以下标记的PTS间断 `EXT-X-DISCONTINUITY` 标记
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* 在支持HTTP重定向和解析JSON的平台上运行。
* 在支持CORS的平台上运行。