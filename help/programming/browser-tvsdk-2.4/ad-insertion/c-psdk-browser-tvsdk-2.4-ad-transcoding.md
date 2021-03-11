---
description: 某些第三方广告（或创意）无法拼接到HTTP实时流(HLS)/HTTP(DASH)内容流上的动态自适应流，因为其视频格式与HLS/DASH不兼容。 Adobe Primetime广告插入和浏览器TVSDK可以选择尝试将不兼容的视频重新打包（转码）到兼容的m3u8/mpd视频中。
title: 重新打包（转码）不兼容的广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 重新打包（转码）不兼容的广告{#repackage-transcode-incompatible-ads}

某些第三方广告（或创意）无法拼接到HTTP实时流(HLS)/HTTP(DASH)内容流上的动态自适应流，因为其视频格式与HLS/DASH不兼容。 Adobe Primetime广告插入和浏览器TVSDK可以选择尝试将不兼容的视频重新打包（转码）到兼容的m3u8/mpd视频中。

来自不同第三方（如代理广告服务器、您的库存合作伙伴或广告网络）的广告通常以不兼容的格式交付，如渐进式下载的MP4。
