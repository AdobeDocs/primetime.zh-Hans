---
description: TVSDK包括用于确定有效速率、当前速率、是否支持特技播放以及与快速前进和倒带相关的其他功能的方法、属性和事件。
title: 费率更改API元素
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# 费率更改API元素 {#rate-change-api-elements}

TVSDK包括用于确定有效速率、当前速率、是否支持特技播放以及与快速前进和倒带相关的其他功能的方法、属性和事件。

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

使用以下API元素更改播放率：

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`，指定有效费率。

| 费率值 | 播放效果 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | 使用指定的乘数快速切换到快进模式（例如，4比正常快4倍） |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | 切换到快速倒带模式 |
| 1.0 | 切换到正常播放模式(调用 `play` 与将rate属性设置为1.0相同) |
| 0.0 | 暂停（调用） `pause` 与将rate属性设置为0.0相同) |
