---
title: 转码和标准化
description: 转码和标准化
copied-description: true
exl-id: 48d9d971-4b15-4f1b-8740-c21983a3e835
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 转码和标准化 {#transcoding-and-normalization}

PrimetimeAd Insertion将尝试通过匹配以下内容，确保跨内容和广告的一致观看体验：

1. 源流编解码器和比特率，同时在转码时始终选择最高质量/比特率创意

1. 源流片段大小(HLS/#EXT-X-TARGETDURATION)

1. 用于转码的首选创意格式

1. 音频自动调平以确保所有广告创意都达到一致的dB级别。

>[!NOTE]
>
>无论内容中定义了哪个HLS版本，PrimetimeAd Insertion生成的HLS资源都会立即转码生成版本3的HLS资源。
