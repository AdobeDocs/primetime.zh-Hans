---
description: 即时转码可以将ID3定时元数据注入广告创意，以便于客户端广告跟踪。
seo-description: 即时转码可以将ID3定时元数据注入HLS格式的广告创意中，以便于客户端广告跟踪。
seo-title: 使用即时转码来注入ID3定时元数据标记
title: 使用即时转码来注入ID3定时元数据标记
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 使用即时转码插入ID3定时元数据标记{#using-crs-to-inject-id-timed-metadata-tags}

CRS可以将ID3定时元数据注入广告创意，以便于客户端广告跟踪。

客户端播放器读取ID3元数据以启用帧精确广告跟踪。

>[!NOTE]
>
>ID3定时元数据注入功能仅用于Safari/iOS。

## ID3注入{#workflow-for-crs-for-id3-injection}的CRS工作流

如果PrimetimeAd Insertion收到`ptplayer=ios-mobileweb`参数，则在上传到相应的广告存储CDN之前，会将ID3数据包注入转码广告创意。
