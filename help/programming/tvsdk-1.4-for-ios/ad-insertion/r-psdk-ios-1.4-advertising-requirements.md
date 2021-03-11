---
title: 广告要求
description: 广告要求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# 广告要求{#advertising-requirements}

您可以使用Adobe Primetime广告决策界面在VOD和实时/线性内容中插入广告。

Primetime广告决策与TVSDK合作，识别广告机会、解析广告并在您的视频流中插入已解析广告。

要在视频内容中加入广告，请确保广告和主要视频内容满足以下要求：

* 广告内容的HLS版本不能高于主内容的HLS版本。
* 广告必须多路传输，并且必须包含纯音频再现，而不管主内容是否多路传输。
* 广告播放列表应具有与主内容播放列表中的再现相同的比特率再现。
* 广告的目标持续时间和单个片段持续时间不能超过主内容的目标持续时间。
* 如果主内容包含纯音频流，则广告内容还必须包含纯音频流。
* 如果主内容包含子标题流，则广告内容必须未加密。
* 如果主内容是多位速率(MBR)，则广告内容也必须是MBR。
* 如果主内容具有替代音轨，则每个广告必须至少具有一个纯音频流。

   如果广告没有至少一个纯音频流，则会跳过广告。