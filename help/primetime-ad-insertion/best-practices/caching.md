---
title: 缓存
description: 缓存
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# HTTP缓存 {#caching}

在获取广告创意以及内容时，PrimetimeAd Insertion默认遵守HTTP缓存控制标头。  这可以显着减少PrimetimeAd Insertion跨所有客户端向CDN发出的网络请求量。  对于缓存，Adobe建议进行以下设置并涉及发送HTTP标头 `max-age` 从您的CDN访问。  请联系您的CDN代表，以在您的视频流和广告流中启用这些标头。

## 对于实时/线性内容 {#caching-live-linear-content}

* 主清单：24小时，或Cache-Control： max-age=86400
* 媒体清单： 1秒，或Cache-Control： max-age=1

## 对于VOD内容 {#caching-vod-content}

* 主清单：24小时，或Cache-Control： max-age=86400
* 媒体清单：24小时，或Cache-Control： max-age=86400
