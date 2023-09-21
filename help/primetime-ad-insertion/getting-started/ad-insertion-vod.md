---
title: 使用VODAd Insertion
description: 使用VOD的Ad Insertion
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 使用VODAd Insertion {#ad-insertion-vod}

PrimetimeAd Insertion支持使用标准VAST 3.0+或VMAP 1.0+格式将广告插入多个VOD资源。

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD（广告地图） {#server-mapped-ads}

PrimetimeAd Insertion支持在开始播放之前使用以VMAP格式定义的广告时间线信息插入广告的VOD插入。  特定于VMAP的广告跟踪（例如breakStart/breakEnd信标）将通过 [广告跟踪](set-up-ad-tracking.md).

## 完整事件重放(包含Ad Decisioning提示的VOD) {#full-event-replay}

PrimetimeAd Insertion还支持在内容流本身中包含提示的特殊VOD资源，例如，在播放之前录制的实时事件时发现的VOD资源。 有关我们支持的广告决策提示（或提示格式）类型的更多信息，请参阅 [在实时/线性中使用Ad Insertion](ad-insertion-live-linear-stream.md).

对于包含多个广告时间的VOD资产，我们支持单个广告请求和并行多个广告请求方案。 有关更多信息，请参阅 `ptmulticall` 中的参数 [参数说明](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md). VAST和VMAP格式都支持流中提示。
