---
description: 如果您的系统可以访问硬件辅助解码，则与使用纯软件TVSDK实现相比，使用iFrame格式可以实现更顺畅的特技播放。
seo-description: 如果您的系统可以访问硬件辅助解码，则与使用纯软件TVSDK实现相比，使用iFrame格式可以实现更顺畅的特技播放。
seo-title: 更流畅的特技播放操作
title: 更流畅的特技播放操作
uuid: 4749bfa0-17bf-4444-a167-987249945325
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 更流畅的特技播放操作 {#smoother-trick-play-operations}

如果您的系统可以访问硬件辅助解码，则与使用纯软件TVSDK实现相比，使用iFrame格式可以实现更顺畅的特技播放。

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

使用iFrame格式会导致特技播放操作不平滑。 更平滑的特技播放操作使用普通（而非iFrame）配置文件、硬件解码支持和增加的帧速率。 不同的硬件辅助解码设备具有不同的功能。 双速要求每秒60帧(FPS)，而四倍速要求120 FPS。

>[!IMPORTANT]
>
>Adobe建议您将较新Android设备的播放速度限制为双倍，而不要将该功能用于较旧的Android设备。

要实现更平滑的特技播放， `ABRControlParameters.maxPlayoutRate` 请设置为所需的正常速度倍数（例如，2.0表示双速）。 如果随后调用 `MediaPlayer.setRate()``maxPlayoutRate`的参数小于或等于您为其设置的值，则TVSDK会使用常规配置文件来实现更流畅的特技播放。 否则，它将使用iFrame配置文件进行滴播操作。
