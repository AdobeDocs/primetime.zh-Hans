---
title: 缓存
description: 缓存
copied-description: true
exl-id: c12c2345-db55-468a-b4b5-5a9e1364a46d
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# HTTP缓存{#caching}

PrimetimeAd Insertion在获取广告创意和内容时默认会考虑HTTP缓存控制标头。  这可以大幅减少PrimetimeAd Insertion向所有客户端CDN发出的网络请求量。  对于缓存，Adobe建议使用以下设置并包括从CDN发送HTTP头`max-age`。  请与CDN代表联系以在您的视频流和广告流上启用这些标题。

## 对于实时/线性内容{#caching-live-linear-content}

* 主控清单：24小时，或缓存控制：max-age=86400
* 媒体清单：1秒，或缓存控制：max-age=1

## 对于VOD内容{#caching-vod-content}

* 主控清单：24小时，或缓存控制：max-age=86400
* 媒体清单：24小时，或缓存控制：max-age=86400
