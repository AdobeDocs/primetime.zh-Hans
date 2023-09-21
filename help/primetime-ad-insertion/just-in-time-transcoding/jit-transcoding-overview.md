---
title: Just-in-Time Transcoding
description: Just-in-Time Transcoding
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Just-in-Time Transcoding {#just-in-time-transcoding}

PrimetimeAd Insertion具有即时的转码和打包功能，可确保不兼容的广告创意内容可以在内容流中正确播放。 它还可以将ID3数据包注入可用于客户端广告跟踪的广告片段。
典型的工作流程如下：

1. Adobe PrimetimeAd Insertion从客户的广告服务器获取广告/创意。

1. 如果广告的创意格式与内容流原生兼容，则创意将插入到清单中。

1. 如果广告的创意格式本身不兼容（例如，.mp4、.mov、.webm），则PrimetimeAd Insertion会从指定的CDN中搜索广告的预编码版本。 如果找到某个广告，则会插入该广告；否则，该广告将排队等待转码。

1. 对广告创意进行转码后，PrimetimeAd Insertion会将该广告资源的所有后续请求合并到清单中。

PrimetimeAd Insertion支持大多数视频和线性格式的转码。 广告创意转码通常在三分钟内发生。 有关更多详细信息，请联系您的Primetime支持代表。
