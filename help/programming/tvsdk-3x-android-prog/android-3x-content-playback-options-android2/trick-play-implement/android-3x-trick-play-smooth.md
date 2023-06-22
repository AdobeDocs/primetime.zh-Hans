---
description: 如果您的系统能够使用硬件辅助解码，则使用iFrame格式即可获得比纯软件TVSDK实施更流畅的特技播放。
title: 更顺畅的戏法操作
exl-id: f69bf480-122b-474d-8f35-31655ea87c70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 更顺畅的戏法操作 {#smoother-trick-play-operations}

如果您的系统能够使用硬件辅助解码，则使用iFrame格式即可获得比纯软件TVSDK实施更流畅的特技播放。

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

使用iFrame格式会导致特技播放操作不平滑。 更平滑的特技播放操作使用标准（非iFrame）配置文件、硬件解码支持和增加的帧速率。 不同的硬件辅助解码设备具有不同的功能。 双速需要60帧/秒(FPS)，四速需要120 FPS。

>[!IMPORTANT]
>
>Adobe建议您将较新Android设备的播放速度限制为两倍，而不要在较旧Android设备上使用功能。

为了达到更流畅的戏法播放，请设置 `ABRControlParameters.maxPlayoutRate` 正常速度的所需倍数（例如，双倍速度为2.0）。 如果对的后续调用 `MediaPlayer.setRate()` 有一个参数小于或等于您设置的值 `maxPlayoutRate`， TVSDK使用普通配置文件实现更平滑的戏法播放。 否则，它使用iFrame配置文件进行点击播放操作。
