---
title: 广告要求
description: 广告要求
copied-description: true
exl-id: 906f4910-396c-4909-8e22-119486ed13a0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 广告要求 {#advertising-requirements}

您可以使用Adobe Primetime广告决策界面在VOD和实时/线性内容中插入广告。

Primetime Ad Decisioning与TVSDK结合使用，以识别广告机会、解决广告并在视频流中插入已解决的广告。

要在视频内容中加入广告，请确保广告和主视频内容满足以下要求：

* 广告内容的HLS版本不能高于主内容的HLS版本。
* 广告必须多路复用，并且必须包含纯音频演绎版，无论主内容是否多路复用。
* 广告播放列表应具有与主内容播放列表中的演绎版相同的比特率。
* 广告的目标持续时间和单个片段持续时间不得超过主内容的目标持续时间。
* 如果主内容包含纯音频流，则广告内容还必须包含纯音频流。
* 如果主内容包含字幕流，则必须对广告内容进行解密。
* 如果主内容是多位速率(MBR)，则广告内容也必须是MBR。
* 如果主内容具有备用音频轨道，则每个广告必须具有至少一个纯音频流。

   如果广告没有至少一个纯音频流，则会跳过该广告。
