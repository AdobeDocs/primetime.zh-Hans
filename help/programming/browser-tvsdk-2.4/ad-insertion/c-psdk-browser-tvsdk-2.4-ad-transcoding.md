---
description: 某些第三方广告（或创意）无法拼合到HTTP实时流(HLS)/HTTP动态自适应流(DASH)内容流中，因为其视频格式与HLS/DASH不兼容。 Adobe Primetime广告插入和浏览器TVSDK可以选择尝试将不兼容的视频重新打包（转码）为兼容的m3u8/mpd视频。
title: 重新打包（转码）不兼容的广告
exl-id: aaa78d5a-4b4b-4d50-b516-d39b47174487
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 重新打包（转码）不兼容的广告{#repackage-transcode-incompatible-ads}

某些第三方广告（或创意）无法拼合到HTTP实时流(HLS)/HTTP动态自适应流(DASH)内容流中，因为其视频格式与HLS/DASH不兼容。 Adobe Primetime广告插入和浏览器TVSDK可以选择尝试将不兼容的视频重新打包（转码）为兼容的m3u8/mpd视频。

由不同的第三方提供的广告，例如代理广告服务器、库存合作伙伴或广告网络，通常以不兼容的格式投放，例如渐进式下载MP4。
