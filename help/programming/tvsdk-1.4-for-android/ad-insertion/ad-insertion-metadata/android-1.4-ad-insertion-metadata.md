---
description: 要允许广告解析程序工作，广告提供商(如Adobe Primetime ad decisioning)需要配置值来启用与提供商的连接。
title: 广告插入元数据
exl-id: 7245b42c-f3ba-43ec-b895-c1a2d66aa11f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 概述 {#ad-insertion-metadata}

要允许广告解析程序工作，广告提供商(如Adobe Primetime ad decisioning)需要配置值来启用与提供商的连接。

TVSDK包括Primetime广告决策库。 要使您的内容包含来自Primetime Ad Decisioning服务器的广告，您的应用程序必须提供以下必需信息 `AuditudeSettings` 信息：

* `mediaID`，这是要播放的视频的唯一标识符。

   发布者分配 `mediaID` 将视频内容和广告信息提交到Adobe Primetime ad decisioning服务器时。 Primetime广告决策使用此ID从服务器检索视频的相关广告信息。

* （可选） `defaultMediaId`，指定满足以下条件时提供的广告：

   * 您向广告服务器发出的请求无效，或内容配置不正确。
   * Primetime ad decisioning在传播数据时遇到延迟。
   * 其中一个Primetime广告决策后端流程出现故障或不可用。

   >[!TIP]
   >
   >Adobe建议使用 `defaultMediaId`.

* 您的 `zoneID`由Adobe分配，用于标识您的公司或网站。
* 您分配的广告服务器的域。
* 其他定位参数。

   您可以根据自己的需求和广告提供商的需求来包含这些参数。
