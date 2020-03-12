---
description: 为了使广告解析程序正常工作，广告提供商（如Adobe Primetime广告决策）需要配置值才能启用与提供商的连接。
seo-description: 为了使广告解析程序正常工作，广告提供商（如Adobe Primetime广告决策）需要配置值才能启用与提供商的连接。
seo-title: 广告插入元数据
title: 广告插入元数据
uuid: 676e81b9-4c2b-487e-bc68-74879ca2966b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 概述 {#ad-nsertion-metadata-overview}

为了使广告解析程序正常工作，广告提供商（如Adobe Primetime广告决策）需要配置值才能启用与提供商的连接。

TVSDK包括Primetime广告决策库。 要使您的内容包含来自Primetime广告决策服务器的广告，您的应用程序必须提供以下必需信 `AuditudeSettings` 息：

* `mediaID`，这是要播放的视频的唯一标识符。

   发布者在将视频内容和广告信息提交到Adobe Primetime广告决策服务器时分配mediaID。 此ID由Primetime广告决策使用，以从服务器检索视频的相关广告信息。

* （可选） `defaultMediaId`，它指定满足以下条件时投放的广告：

   * 您对广告服务器的请求无效，或内容配置不正确。
   * Primetime广告决策在传播数据方面遇到了延误。
   * Primetime广告决策后端进程之一发生故障或不可用。
   >[!TIP]
   >
   >Adobe建议使用 `defaultMediaId`。

* 由Adobe `zoneID`指定的您的公司或网站。
* 您分配的广告服务器的域。
* 其他定位参数。

   您可以根据您的需求和广告提供商的需求包含这些参数。