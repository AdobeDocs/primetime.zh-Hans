---
description: 即时转码功能可以将ID3定时元数据注入广告创意，以便于客户端广告跟踪。
title: 使用即时转码来插入ID3定时元数据标记
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 使用即时转码来插入ID3定时元数据标记{#using-crs-to-inject-id-timed-metadata-tags}

CRS可以将ID3定时元数据注入广告创意，以便于客户端广告跟踪。

客户端播放器读取ID3元数据以启用帧精确广告跟踪。

>[!NOTE]
>
>ID3定时元数据注入功能仅适用于Safari/iOS。

## ID3注入{#workflow-for-crs-for-id3-injection}的CRS工作流

如果PrimetimeAd Insertion收到`ptplayer=ios-mobileweb`参数，它将在上传到相应的广告存储CDN之前，将ID3数据包注入转码广告创意。
