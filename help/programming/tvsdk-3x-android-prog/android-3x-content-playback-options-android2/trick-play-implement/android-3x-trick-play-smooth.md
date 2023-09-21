---
description: 如果您的系统能够访问硬件辅助解码，那么与使用iFrame格式的纯软件TVSDK实施相比，您可以获得更流畅的特技播放。
title: 更流畅的特技游戏操作
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 更流畅的特技游戏操作 {#smoother-trick-play-operations}

如果您的系统能够访问硬件辅助解码，那么与使用iFrame格式的纯软件TVSDK实施相比，您可以获得更流畅的特技播放。

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

使用iFrame格式会导致不平滑的特技播放操作。 更平滑的特技播放操作使用标准（非iFrame）配置文件、硬件解码支持和增加的帧速率。 不同的硬件辅助解码设备具有不同的功能。 双速需要60帧/秒(FPS)，四速需要120 FPS。

>[!IMPORTANT]
>
>Adobe建议您将较新Android设备的播放速度限制为双倍，而不要在较旧Android设备上使用功能。

若要获得更流畅的魔术游戏，请设置 `ABRControlParameters.maxPlayoutRate` 正常速度的所需倍数（例如，双速为2.0）。 如果对的后续调用 `MediaPlayer.setRate()` 有一个参数小于或等于您为设置的值 `maxPlayoutRate`， TVSDK使用普通配置文件来实现更流畅的特技播放。 否则，它使用iFrame配置文件进行点击播放操作。
