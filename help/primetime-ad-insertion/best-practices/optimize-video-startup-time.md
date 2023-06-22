---
title: 优化视频启动时间
description: 优化视频启动时间
exl-id: 5a89c774-0fed-4378-9cf8-98c4c843ae0d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 优化视频启动时间概述 {#optimize-video-start-up-times}

PrimetimeAd Insertion提供多种功能以优化视频启动时间，例如缓存和路由/协议优化规则。 以下是使用PrimetimeAd Insertion时为确保视频更快启动而提出的一些其他建议：

* 提供内容交付网络(CDN)中的所有广告和内容

* 减少或删除PrimetimeAd Insertion与CDN之间的TLS握手。 有关更多信息，请参阅 [优化路由和协议](optimize-routes-protocols.md).

* 从同一CDN提供广告和内容片段

* 为实时/VOD内容和清单插入cache-control标头

* 减少或删除响应缓慢的广告提供商或广告创意
