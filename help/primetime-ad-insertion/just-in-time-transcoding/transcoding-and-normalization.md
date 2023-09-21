---
title: 转码和标准化
description: 转码和标准化
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 转码和标准化 {#transcoding-and-normalization}

PrimetimeAd Insertion将尝试通过匹配以下内容，以确保在内容和广告之间获得一致的观看体验：

1. 源流编解码器和比特率，同时在转码时始终选择最高质量/比特率创意

1. 源流片段大小(HLS/#EXT-X-TARGETDURATION)

1. 用于转码的首选创意格式

1. 音频自动调平可确保所有广告创意均达到一致的dB级别。

>[!NOTE]
>
>无论内容中定义了哪个HLS版本，PrimetimeAd Insertion生成的HLS资源都会立即转码生成版本3的HLS资源。
