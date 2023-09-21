---
title: Adobe PrimetimeAd Insertion入门
description: Adobe PrimetimeAd Insertion快速入门
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Adobe PrimetimeAd Insertion入门 {#ptai-get-started}

PrimetimeAd Insertion协调提供内容和广告的系统，以创建个性化的流中广告体验，然后跟踪广告商的广告播放。

PrimetimeAd Insertion通过重写视频清单来与视频交付客户端应用程序交互，从而为每个查看者提供有针对性的广告和个性化体验。 这些清单将内容和从广告服务器投放的广告相结合，并且可以选择包括包含详细广告跟踪指令的元数据。 PrimetimeAd Insertion支持客户端和服务器端广告跟踪。

正确设置系统后，典型的工作流可能如下所示：

1. 客户端应用程序生成 [BOOTSTRAPURL](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) 其中包含有关视频流的信息并向PrimetimeAd Insertion发送GET请求。  PrimetimeAd Insertion支持各种广告信令格式的HLS和DASH。

1. PrimetimeAd Insertion将通过将内容清单从发布者的CDN发送回客户端应用程序来进行响应。

1. 客户端应用程序在生成的清单中选择要播放的合适流，并向PrimetimeAd Insertion发出请求。

1. PrimetimeAd Insertion从内容CDN获取请求的流，解析/读取任何提示信息，调用广告服务器并根据需要替换广告时间。

1. PrimetimeAd Insertion通过重写资源URL并检测广告创意是否需要转码来标准化清单，请参阅 [Just-in-time Ad Transcoding](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md).

1. PrimetimeAd Insertion会获取所需的广告创意，并将相应的片段插入到清单中。

1. PrimetimeAd Insertion将最终的拼接清单（包括广告）交付给客户端应用程序进行播放。

1. 广告投放和可见性可以通过客户端或服务器端广告跟踪进行测量，请参阅 [设置广告跟踪](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md).

PrimetimeAd Insertion支持大多数HLS/DASH客户端和播放器配置。 有关支持的特定广告信号格式的更多信息，请参阅 [支持的提示格式](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md).
