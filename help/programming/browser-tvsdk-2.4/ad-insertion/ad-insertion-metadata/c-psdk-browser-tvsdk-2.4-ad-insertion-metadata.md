---
description: 要允许广告解析程序工作，广告提供商(如Adobe Primetime ad decisioning)需要配置值来启用与提供商的连接。
title: 广告插入元数据
exl-id: 8d6cb371-8666-4b55-b828-0f1d495e7fb7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 概述 {#ad-insertion-metadata-overview}

要允许广告解析程序工作，广告提供商(如Adobe Primetime ad decisioning)需要配置值来启用与提供商的连接。

浏览器TVSDK包含Adobe Primetime广告决策库。 要使您的内容包含来自Adobe Primetime ad decisioning服务器的广告，您的应用程序必须提供以下必需的AudienceSettings信息：

* `mediaID`，这是要播放的视频的唯一标识符。

   在将视频内容和广告信息提交到Adobe Primetime广告决策服务器时，发布者会分配mediaID。 Adobe Primetime ad decisioning使用此ID从服务器检索视频的相关广告信息。

* （可选） `defaultMediaId`，指定满足以下条件时提供的广告：

   * 您向广告服务器发出的请求无效，或内容配置不正确。
   * Adobe Primetime ad decisioning在传播数据时遇到延迟。
   * 其中一个Adobe Primetime ad decisioning后端流程出现故障或不可用。

   >[!TIP]
   >
   >Adobe建议使用 `defaultMediaId`.

* 您的 `zoneID`由Adobe分配，用于标识您的公司或网站。
* 您分配的广告服务器的域。
* 其他定位参数。

   您可以根据自己的需求和广告提供商的需求来包含这些参数。
