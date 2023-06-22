---
title: 实时转码
description: 实时转码
copied-description: true
exl-id: 9577e1d5-1462-49d6-9d24-94e74dc9c019
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 实时转码 {#just-in-time-transcoding}

PrimetimeAd Insertion具有及时转码和打包功能，可确保不兼容的广告创意在内容流中正确播放。 它还可以将ID3数据包注入可用于客户端广告跟踪的广告片段中。
典型的工作流程如下：

1. Adobe PrimetimeAd Insertion从客户的广告服务器获取广告/创意。

1. 如果广告的创意格式与内容流原生兼容，则创意将插入到清单中。

1. 如果广告的创意格式本身不兼容（例如.mp4、.mov、.webm），则PrimetimeAd Insertion会从指定的CDN中搜索广告的预转码版本。 如果找到某个广告，则会插入该广告；否则，该广告将排队等待转码。

1. 对广告创意进行转码后，PrimetimeAd Insertion会将该广告资源的所有后续请求合并到清单中。

PrimetimeAd Insertion支持大多数视频和线性格式的转码。 广告创意转码通常在三分钟内发生。 有关更多详细信息，请联系您的Primetime支持代表。
