---
description: 所有视频播放器都必须提供清单服务器赖以插入广告和启用广告跟踪的功能。
seo-description: 所有视频播放器都必须提供清单服务器赖以插入广告和启用广告跟踪的功能。
seo-title: 视频播放器要求
title: 视频播放器要求
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# 视频播放器要求{#video-player-requirements}

所有视频播放器都必须提供清单服务器赖以插入广告和启用广告跟踪的功能。

要使用Primetime广告插入API，视频播放器必须满足以下条件：

* 可以在回放内容时跟踪播放头位置。
* 可以在指定的时间请求跟踪URL。
* 在支持HLS v3或更高版本的设备平台上运行，包括：

   * 标记为`EXT-X-DISCONTINUITY`的PTS不连续
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* 在支持HTTP重定向和解析JSON的平台上运行。
* 基于Web的播放器必须在支持CORS的平台上运行。