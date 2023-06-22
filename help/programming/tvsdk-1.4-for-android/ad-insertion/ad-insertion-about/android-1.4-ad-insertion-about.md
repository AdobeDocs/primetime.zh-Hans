---
description: 广告插入可解析用于视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流的广告。 TVSDK向广告服务器发出所需请求，接收有关指定内容的广告信息，并将广告分阶段放入内容中。
title: 插入广告
exl-id: 390036e2-2459-4cfb-a336-640d816bdaad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# 概述 {#insert-ads-overview}

广告插入可解析用于视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流的广告。 TVSDK向广告服务器发出所需请求，接收有关指定内容的广告信息，并将广告分阶段放入内容中。

广告时间包含一个或多个按顺序播放的广告。 TVSDK将广告作为一个或多个广告时间的成员，插入主内容中。

>[!TIP]
>
>如果广告有错误，TVSDK会忽略该广告。
