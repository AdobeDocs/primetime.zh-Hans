---
description: 要允许广告解析程序工作，广告提供商(如Adobe Primetime广告决策)需要配置值以启用与提供商的连接。
title: 广告插入元数据
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# 概述{#ad-insertion-metadata}

要允许广告解析程序工作，广告提供商(如Adobe Primetime广告决策)需要配置值以启用与提供商的连接。

TVSDK包括Primetime广告决策库。 要使您的内容包括来自Primetime广告决策服务器的广告，您的应用程序必须提供以下必需的`AuditudeSettings`信息：

* `mediaID`，这是要播放的视频的唯一标识符。

   发布者在向Adobe Primetime广告决策服务器提交视频内容和广告信息时分配`mediaID`。 此ID由Primetime广告决策用来从服务器检索视频的相关广告信息。

* （可选）`defaultMediaId`，它指定满足以下条件时投放的广告：

   * 您对广告服务器的请求无效，或内容配置不正确。
   * Primetime广告决策在传播数据时遇到延迟。
   * Primetime广告决策后端进程之一出现故障或不可用。

   >[!TIP]
   >
   >Adobe建议使用`defaultMediaId`。

* 由Adobe分配的`zoneID`标识您的公司或网站。
* 您分配的广告服务器的域。
* 其他定位参数。

   您可以根据您的需求和广告提供商的需求包含这些参数。