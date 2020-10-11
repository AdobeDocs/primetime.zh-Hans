---
title: 使用Ad Insertion进行VOD
description: 将Ad Insertion用于VOD
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# 使用Ad Insertion进行VOD {#ad-insertion-vod}

PrimetimeAd Insertion使用标准VAST 3.0+或VMAP 1.0+格式支持广告插入多个VOD资产。

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD（服务器映射的广告） {#server-mapped-ads}

PrimetimeAd Insertion支持在播放开始前插入广告的VOD插入，广告时间线信息以VMAP格式定义。  特定于VMAP的广告跟踪（如breakStart/breakEnd信标）将随广告跟踪 [一起提供](set-up-ad-tracking.md)。

## 完整事件重播(带有Ad Decisioning提示的VOD) {#full-event-replay}

PrimetimeAd Insertion还支持包含内容流本身提示的专用VOD资产，如回放以前录制的实时事件。 有关我们支持的广告决策提示（或提示格式）类型的更多信息，请参 [阅在实时／线性中使用Ad Insertion](ad-insertion-live-linear-stream.md)。

对于包含多个广告分段的VOD资产，我们支持单个广告请求和并行的多个广告请求方案。 有关详细信息，请参 `ptmulticall` 阅参数 [说明中的参数](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)。 VAST和VMAP格式均支持流内提示。
