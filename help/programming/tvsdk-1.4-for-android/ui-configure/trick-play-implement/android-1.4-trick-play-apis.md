---
description: TVSDK包括用于确定有效速率、当前速率、是否支持特技播放以及与快速前进和倒带相关的其他功能的方法、属性和事件。
title: 费率更改API元素
exl-id: 9c366645-5ce5-485c-8423-cb0ed4bd2677
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# 费率更改API元素{#rate-change-api-elements}

TVSDK包括用于确定有效速率、当前速率、是否支持特技播放以及与快速前进和倒带相关的其他功能的方法、属性和事件。

<!--<a id="section_36576E92DE6343AEBD0BBD662502365D"></a>-->

使用以下API元素更改播放率：

* `PlaybackRateEvent.getRate`
* `MediaPlayer.getLocalTime`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.getAvailablePlaybackRates`  — 指定有效费率。

| 费率值 | 对播放的影响 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | 使用指定的乘数快速切换到快进模式（例如，4比正常快4倍） |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | 切换到快速倒带模式 |
| 1.0 | 切换到正常播放模式(呼叫 `play` 与将rate属性设置为1.0相同) |
| 0.0 | 暂停（调用） `pause` 与将rate属性设置为0.0相同) |
