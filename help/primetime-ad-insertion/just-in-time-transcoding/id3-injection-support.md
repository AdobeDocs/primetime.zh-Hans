---
description: 即时转码可以将ID3定时元数据插入到广告创意中，以促进客户端广告跟踪。
title: 使用即时转码插入ID3定时元数据标记
exl-id: 6171223a-71f9-45a2-a3f5-7ede4a9b101a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 使用即时转码插入ID3定时元数据标记 {#using-crs-to-inject-id-timed-metadata-tags}

CRS可以将ID3定时元数据插入到广告创意中，以促进客户端广告跟踪。

客户端播放器读取ID3元数据以启用帧准确的广告跟踪。

>[!NOTE]
>
>ID3定时元数据注入功能仅适用于Safari/iOS。

## 用于ID3注入的CRS的工作流 {#workflow-for-crs-for-id3-injection}

如果PrimetimeAd Insertion收到 `ptplayer=ios-mobileweb` 参数，它会先将ID3数据包注入转码广告创意，然后再上传到相应的广告存储CDN。
