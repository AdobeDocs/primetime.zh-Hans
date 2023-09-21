---
description: 广告插入可解析用于视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流的广告。 TVSDK向广告服务器发出所需请求，接收有关指定内容的广告信息，并将广告分阶段放入内容中。
title: 插入广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 概述 {#insert-ads-overview}

广告插入可解析用于视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流的广告。 TVSDK向广告服务器发出所需请求，接收有关指定内容的广告信息，并将广告分阶段放入内容中。

An *`ad break`* 包含一个或多个按顺序播放的广告。 TVSDK会将广告作为一个或多个广告时间的成员，插入主内容中。

>[!NOTE]
>
>如果广告有错误，TVSDK会忽略该广告。
