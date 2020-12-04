---
description: 所有视频播放器都必须提供清单服务器赖以插入广告和启用广告跟踪的功能。
seo-description: 所有视频播放器都必须提供清单服务器赖以插入广告和启用广告跟踪的功能。
seo-title: 视频播放器要求
title: 视频播放器要求
uuid: 29593d67-2901-4d9e-a08f-23c8a7667283
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '136'
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
* 在支持CORS的平台上运行。