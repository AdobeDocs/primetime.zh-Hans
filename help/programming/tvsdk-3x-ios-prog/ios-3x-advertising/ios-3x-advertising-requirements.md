---
description: 您可以使用Adobe Primetime广告决策界面在VOD和实时／线性内容中插入广告。
seo-description: 您可以使用Adobe Primetime广告决策界面在VOD和实时／线性内容中插入广告。
seo-title: 广告要求
title: 广告要求
uuid: 0287f1e4-746f-42e5-b811-409064dd9b13
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# 广告要求{#advertising-requirements}

您可以使用Adobe Primetime广告决策界面在VOD和实时／线性内容中插入广告。

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

Primetime广告决策与TVSDK协同工作，以识别广告机会、解析广告并在您的视频流中插入已解析的广告。

要在视频内容中加入广告，请确保广告和主视频内容满足以下要求：

* 广告内容的HLS版本不能高于主内容的HLS版本。
* 广告必须进行多路复用，并且必须包含纯音频再现，无论主内容是否进行多路复用。
* 广告播放列表的比特率再现应与主内容播放列表中的再现相同。
* 广告的目标持续时间和单个片段持续时间不能超过主内容的目标持续时间。
* 如果主内容包含纯音频流，则广告内容还必须包含纯音频流。
* 如果主内容包含子标题流，则广告内容必须未加密。
* 如果主要内容是多比特率(MBR)，则广告内容也必须是MBR。
* 如果主内容有替代的音轨，则每个广告必须至少有一个纯音频流。

如果广告至少没有一个纯音频流，则会跳过广告。