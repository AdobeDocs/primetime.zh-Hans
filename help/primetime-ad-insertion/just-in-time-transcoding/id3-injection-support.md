---
description: 实时转码可以将ID3定时元数据注入广告创意中以方便客户端广告跟踪。
title: 使用即时代码转换插入ID3定时元数据标记
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 使用及时转码插入ID3定时元数据标记 {#using-crs-to-inject-id-timed-metadata-tags}

CRS可以将ID3定时元数据注入广告创意中以方便客户端广告跟踪。

客户端播放器读取ID3元数据以启用帧准确的广告跟踪。

>[!NOTE]
>
>ID3定时元数据注入仅适用于Safari/iOS。

## 适用于ID3注入的CRS的工作流 {#workflow-for-crs-for-id3-injection}

如果PrimetimeAd Insertion收到 `ptplayer=ios-mobileweb` 参数，它会先将ID3数据包注入转码广告创意，然后再上传到相应的广告存储CDN。
