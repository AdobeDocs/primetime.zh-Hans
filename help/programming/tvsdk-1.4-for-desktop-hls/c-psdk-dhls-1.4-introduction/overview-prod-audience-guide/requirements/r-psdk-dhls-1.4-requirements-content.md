---
description: 检查流和播放列表（清单）的限制和要求，包括DRM加密密钥。
title: 内容和清单要求
exl-id: 96b2b245-558b-4606-87c0-22140430c326
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# 内容和清单要求 {#content-and-manifest-requirements}

检查流和播放列表（清单）的限制和要求，包括DRM加密密钥。

| 包含并设置 `RESOLUTION` 清单文件中每个ABR流的属性。 必须使用Flash Player14或更高版本。 |
|---|
| 如果受DRM保护的流是多比特率(MBR)，则用于MBR的DRM加密密钥应与用于所有比特率流中的密钥相同。 |
| 必须具有与主内容的演绎版相同的比特率演绎版。 |
