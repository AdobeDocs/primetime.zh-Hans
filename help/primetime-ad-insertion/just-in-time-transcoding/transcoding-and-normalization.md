---
title: 转码和标准化
description: null
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# 转码和标准化{#transcoding-and-normalization}

PrimetimeAd Insertion将尝试通过匹配以下内容和广告来确保一致的观看体验：

1. 源流编解码器和比特率，同时在转码时始终选择最高质量／比特率的创意

1. 源流片段大小(HLS/#EXT-X-TARGETDURATION)

1. 用于转码的首选创意格式

1. 音频自动调平可确保所有广告创意的dB级别一致。

>[!NOTE]
>
>由PrimetimeAd Insertion的即时转码生成的HLS资产会生成版本3的HLS资产，而不管内容中定义的HLS版本。