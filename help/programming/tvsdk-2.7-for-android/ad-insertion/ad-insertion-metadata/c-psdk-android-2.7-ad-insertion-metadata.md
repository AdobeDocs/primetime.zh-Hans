---
description: 要允许广告解析程序工作，广告提供商(如Adobe Primetime ad decisioning)需要配置值来启用与提供商的连接。
title: 广告插入元数据
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 概述 {#ad-insertion-metadata-overview}

要允许广告解析程序工作，广告提供商(如Adobe Primetime ad decisioning)需要配置值来启用与提供商的连接。

TVSDK包括Primetime ad decisioninglibrary。 要使您的内容包含来自Primetime ad decisioningserver的广告，您的应用程序必须提供以下必需信息 `AuditudeSettings` 信息：

* `mediaID`，要播放的视频的唯一标识符。

  在将视频内容和广告信息提交到Adobe Primetime广告决策服务器时，发布者会分配mediaID。 Primetime ad Decisioning使用此ID从服务器检索视频的相关广告信息。

* （可选） `defaultMediaId`，指定满足以下条件时提供的广告：

   * 您向广告服务器发出的请求无效，或内容配置不正确。
   * Primetime ad decisioning在传播数据时遇到延迟问题。
   * 其中一个Primetime ad Decisioning后端进程出现故障或不可用。

  >[!TIP]
  >
  >Adobe建议使用 `defaultMediaId`.

* 您的 `zoneID`由Adobe分配，用于标识您的公司或网站。
* 您分配的广告服务器的域。
* 其他定位参数。

  您可以根据自己的需要和广告提供商的需求包含这些参数。
