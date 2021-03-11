---
description: 如果您的系统可以访问硬件辅助解码，则与使用纯软件TVSDK实现相比，使用iFrame格式可以实现更流畅的特技播放。
title: 更流畅的特技播放操作
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# 更流畅的特技播放操作{#smoother-trick-play-operations}

如果您的系统可以访问硬件辅助解码，则与使用纯软件TVSDK实现相比，使用iFrame格式可以实现更流畅的特技播放。

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

使用iFrame格式会导致特技播放操作不流畅。 更平滑的特技播放操作使用普通（而非iFrame）用户档案、硬件解码支持和增加的帧速率。 不同的硬件辅助解码设备具有不同的功能。 多次速度要求每秒60帧(FPS)，而四帧速度要求每秒120 FPS。

>[!IMPORTANT]
>
>Adobe建议您将较新Android设备的播放速度限制为多次速度，而不要对较旧的Android设备使用该功能。

要实现更平滑的特技播放，请将`ABRControlParameters.maxPlayoutRate`设置为所需的正常速度倍数(例如，2.0表示多次速度)。 如果对`MediaPlayer.setRate()`的后续调用的参数小于或等于您为`maxPlayoutRate`设置的值，则TVSDK使用普通用户档案来实现更流畅的特技播放。 否则，它使用iFrame用户档案进行滴播操作。