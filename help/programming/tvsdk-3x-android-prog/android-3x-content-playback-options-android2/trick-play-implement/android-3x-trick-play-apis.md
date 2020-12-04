---
description: TVSDK包括确定有效率、当前速率、技巧播放是否受支持以及与快速前进和后退相关的其他功能的方法、属性和事件。
seo-description: TVSDK包括确定有效率、当前速率、技巧播放是否受支持以及与快速前进和后退相关的其他功能的方法、属性和事件。
seo-title: 速率更改API元素
title: 速率更改API元素
uuid: c2bcd20c-0641-4d75-802c-08098786d572
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 2%

---


# 速率更改API元素{#rate-change-api-elements}

TVSDK包括确定有效率、当前速率、技巧播放是否受支持以及与快速前进和后退相关的其他功能的方法、属性和事件。

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

使用以下API元素更改播放率：

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`，它指定有效率。

| **比率值** | **播放效果** |
|---|---|
| 2.0、4.0、8.0、16.0、32.0、64.0、128.0 | 切换到快进模式时，指定的乘法器比正常速度快（例如，4比正常速度快4倍） |
| -2.0、-4.0、-8.0、-16.0、-32.0、-64.0、-128.0 | 切换到快速后退模式 |
| 1.0 | 切换为正常播放模式（调用`play`与将速率属性设置为1.0相同） |
| 0.0 | 暂停（调用`pause`与将速率属性设置为0.0相同） |