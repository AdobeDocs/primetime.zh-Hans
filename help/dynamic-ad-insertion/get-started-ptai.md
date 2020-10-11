---
title: 开始使用Adobe PrimetimeAd Insertion
description: Adobe PrimetimeAd Insertion入门
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# 开始使用Adobe PrimetimeAd Insertion {#ptai-get-started}

PrimetimeAd Insertion协调提供内容和广告的系统，以创建个性化的流内广告体验，然后跟踪广告商的广告播放。

PrimetimeAd Insertion通过重写视频清单与视频投放客户端应用程序交互，为每个观众提供有针对性的广告和个性化体验。这些清单结合了从广告服务器发送的内容和广告，并可以选择包含详细广告跟踪说明的元数据。 PrimetimeAd Insertion支持客户端和服务器端广告跟踪。

正确设置系统后，典型的工作流可能如下所示：

1. 客户端应用程序生 [成BootstrapURL](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md) ，其中包含有关视频流的信息，并向PrimetimeAd Insertion发送GET请求。

1. PrimetimeAd Insertion通过将内容清单从出版商的CDN发回客户端应用程序来做出响应。

1. 客户端应用程序在生成的清单中选择适当的流来播放，并向PrimetimeAd Insertion发出请求。

1. PrimetimeAd Insertion从内容CDN获取所请求的流，分析／读取任何提示信息，向广告服务器发出调用，并根据需要替换广告分段。

1. PrimetimeAd Insertion通过重写资源URL并检测广告创意人员是否需要转码来规范清单，请 [参阅即时广告转码](just-in-time-transcoding.md)[和打包](just-in-time-repackaging.md)。

1. PrimetimeAd Insertion获取所需的广告创意，并将适当的片段插入清单。

1. PrimetimeAd Insertion将包括广告在内的最终拼接清单交付给客户端应用程序进行回放。

1. 广告投放和可查看性可通过客户端广告跟踪或服务器端广告跟踪来衡量，请 [参阅设置广告跟踪](set-up-ad-tracking.md)。

PrimetimeAd Insertion支持HLS/DASH的大多数客户端配置。
