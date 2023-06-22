---
title: 缓存
description: 缓存
copied-description: true
exl-id: c12c2345-db55-468a-b4b5-5a9e1364a46d
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# HTTP缓存 {#caching}

默认情况下，PrimetimeAd Insertion在获取广告创意以及内容时遵循HTTP缓存控制标头。  这可以显着减少PrimetimeAd Insertion跨所有客户端向CDN发出的网络请求量。  对于缓存，Adobe建议进行以下设置并涉及发送HTTP标头 `max-age` 从您的CDN.  请联系您的CDN代表，以在您的视频流和广告流上启用这些标头。

## 对于实时/线性内容 {#caching-live-linear-content}

* 主控清单：24小时，或Cache-Control： max-age=86400
* 媒体清单： 1秒，或Cache-Control： max-age=1

## 对于VOD内容 {#caching-vod-content}

* 主控清单：24小时，或Cache-Control： max-age=86400
* 媒体清单：24小时，或Cache-Control： max-age=86400
