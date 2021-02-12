---
title: 即时转码
description: null
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# 即时转码{#just-in-time-transcoding}

PrimetimeAd Insertion功能及时转码和打包，可确保在内容流中正确播放不兼容的广告创意。 它还可以将ID3数据包注入广告片段，以便用于客户端广告跟踪。
典型的工作流如下：

1. Adobe PrimetimeAd Insertion从客户的广告服务器获取广告／创意。

1. 如果广告的创意格式与内容流本机兼容，则创意将插入清单。

1. 如果广告的创意格式本机不兼容（如。mp4、.mov、.webm）,PrimetimeAd Insertion会从指定CDN搜索预转码版本的广告。 如果找到一则广告，则插入该广告；否则，广告将排队等待转码。

1. 转码广告创意后，PrimetimeAd Insertion会将该广告资产的所有后续请求整合到清单中。

PrimetimeAd Insertion支持大多数视频和线性格式的转码。 广告创意转码通常在三分钟内完成。 有关更多详细信息，请联系您的Primetime支持代表。
