---
title: 缓存
description: null
translation-type: tm+mt
source-git-commit: 76dc54fabdae400ad708ba83fcf6f7fd5caa2b22
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# HTTP缓存{#caching}

PrimetimeAd Insertion在提取广告创意和内容时默认遵循HTTP缓存控制标头。  这可以大幅减少PrimetimeAd Insertion向所有客户端CDN发出的网络请求量。  对于缓存，Adobe建议使用以下设置并涉及从CDN发送HTTP头`max-age`。  请与CDN代表联系，在您的视频流和广告流中启用这些标题。

## 对于实时／线性内容{#caching-live-linear-content}

* 主控清单：24小时，或缓存控制：max-age=86400
* 媒体清单：1秒，或缓存控制：max-age=1

## 对于VOD内容{#caching-vod-content}

* 主控清单：24小时，或缓存控制：max-age=86400
* 媒体清单：24小时，或缓存控制：max-age=86400
