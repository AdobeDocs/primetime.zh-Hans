---
title: 开始使用Adobe PrimetimeAd Insertion
description: Adobe PrimetimeAd Insertion入门
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# 开始使用Adobe PrimetimeAd Insertion{#ptai-get-started}

PrimetimeAd Insertion协调提供内容和广告的系统，以创建个性化的流内广告体验，然后跟踪广告商的广告播放。

PrimetimeAd Insertion通过重写视频清单与视频投放客户端应用程序交互，为每位观众提供有针对性的广告和个性化体验。 这些清单将从广告服务器提供的内容和广告结合在一起，并可以选择包括包含详细广告跟踪说明的元数据。 PrimetimeAd Insertion支持客户端和服务器端广告跟踪。

正确设置系统后，典型的工作流可能如下所示：

1. 客户端应用程序生成具有视频流相关信息的[BootstrapURL](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)，并向PrimetimeAd Insertion发送GET请求。  PrimetimeAd Insertion支持HLS和DASH的各种广告信号格式。

1. PrimetimeAd Insertion通过将内容清单从出版商的CDN发回客户端应用程序来做出响应。

1. 客户端应用程序在生成的清单中选择适当的流来播放，并向PrimetimeAd Insertion发出请求。

1. PrimetimeAd Insertion从内容CDN获取所请求的流，分析／读取任何提示信息，向广告服务器发出调用，并根据需要替换广告分段。

1. PrimetimeAd Insertion通过重写资源URL并检测广告创意人员是否需要转码来标准化清单，请参阅[即时广告转码](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md)。

1. PrimetimeAd Insertion获取所需的广告创意，并将适当的片段插入清单。

1. PrimetimeAd Insertion将包括广告在内的最终拼接清单交付给客户端应用程序进行回放。

1. 广告投放和可见性可通过客户端广告跟踪或服务器端广告跟踪来衡量，请参阅[设置广告跟踪](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md)。

PrimetimeAd Insertion支持大多数HLS/DASH客户端和播放器配置。 有关支持的特定广告信号格式的详细信息，请参见[支持的提示格式](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md)。
