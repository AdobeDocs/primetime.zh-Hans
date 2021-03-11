---
description: 检查流和播放列表（清单）（包括DRM加密密钥）的限制和要求。
title: 内容和清单要求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# 内容和清单要求{#content-and-manifest-requirements}

检查流和播放列表（清单）（包括DRM加密密钥）的限制和要求。

| 在清单文件中包括并设置每个ABR流的`RESOLUTION`属性。 必须使用Flash Player 14或更高版本。 |
|---|
| 如果受DRM保护的流是多比特率(MBR)，则用于MBR的DRM加密密钥应与所有比特率流中使用的密钥相同。 |
| 必须具有与主内容的再现相同的位速率再现。 |