---
description: 为了使广告解析程序正常工作，广告提供商（如Adobe Primetime广告决策）需要配置值才能启用与提供商的连接。
seo-description: 为了使广告解析程序正常工作，广告提供商（如Adobe Primetime广告决策）需要配置值才能启用与提供商的连接。
seo-title: 广告插入元数据
title: 广告插入元数据
uuid: 8848c939-1f12-4145-8025-453b4fe79aae
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 概述 {#ad-insertion-metadata-overview}

为了使广告解析程序正常工作，广告提供商（如Adobe Primetime广告决策）需要配置值才能启用与提供商的连接。

浏览器TVSDK包括Adobe Primetime广告决策库。 要使您的内容包含Adobe Primetime广告决策服务器的广告，您的应用程序必须提供以下必需的AuditudeSettings信息：

* `mediaID`，这是要播放的视频的唯一标识符。

   发布者在将视频内容和广告信息提交到Adobe Primetime广告决策服务器时分配mediaID。 此ID由Adobe Primetime广告决策使用，从服务器检索视频的相关广告信息。

* （可选） `defaultMediaId`，它指定满足以下条件时投放的广告：

   * 您对广告服务器的请求无效，或内容配置不正确。
   * Adobe Primetime广告决策在传播数据时遇到延迟。
   * Adobe Primetime广告决策后端进程之一发生故障或不可用。
   >[!TIP]
   >
   >Adobe建议使用 `defaultMediaId`。

* 由Adobe `zoneID`指定的您的公司或网站。
* 您分配的广告服务器的域。
* 其他定位参数。

   您可以根据您的需求和广告提供商的需求包含这些参数。