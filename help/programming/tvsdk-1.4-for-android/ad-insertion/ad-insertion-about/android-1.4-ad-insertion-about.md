---
description: 广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需请求，接收指定内容的广告信息，并分阶段将广告放入内容中。
title: 插入广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# 概述{#insert-ads-overview}

广告插入解决了视频点播(VOD)、实时流以及带有广告跟踪和广告播放的线性流广告。 TVSDK向广告服务器发出所需请求，接收指定内容的广告信息，并分阶段将广告放入内容中。

广告分段包含一个或多个按顺序播放的广告。 TVSDK将广告作为一个或多个广告分段的成员插入主内容中。

>[!TIP]
>
>如果广告有错误，TVSDK将忽略该广告。