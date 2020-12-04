---
description: 检查流和播放列表（清单）（包括DRM加密密钥）的限制和要求。
seo-description: 检查流和播放列表（清单）（包括DRM加密密钥）的限制和要求。
seo-title: 内容和清单要求
title: 内容和清单要求
uuid: 53cc570a-be33-4488-95e8-43f91b559b13
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# 内容和清单要求{#content-and-manifest-requirements}

检查流和播放列表（清单）（包括DRM加密密钥）的限制和要求。

| 在清单文件中包括并设置每个ABR流的`RESOLUTION`属性。 必须使用Flash Player14或更高版本。 |
|---|
| 如果受DRM保护的流是多比特率(MBR)，则用于MBR的DRM加密密钥应与所有比特率流中使用的密钥相同。 |
| 必须具有与主内容的演绎版相同的比特率演绎版。 |