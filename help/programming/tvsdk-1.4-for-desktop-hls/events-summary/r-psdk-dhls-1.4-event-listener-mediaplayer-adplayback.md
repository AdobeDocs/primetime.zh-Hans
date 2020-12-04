---
description: TVSDK根据广告相关操作(如当广告开始播放时)调度广告播放事件。
seo-description: TVSDK根据广告相关操作(如当广告开始播放时)调度广告播放事件。
seo-title: 广告播放事件
title: 广告播放事件
uuid: 63138237-2315-45ff-914d-369da18fdff7
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# 广告播放事件{#ad-playback-events}

TVSDK根据广告相关操作(如当广告开始播放时)调度广告播放事件。

要获得有关所有广告播放相关事件的通知，请向`MediaPlayer`对象注册以下事件的监听器。

>[!TIP]
>
>当广告插入媒体或从媒体中删除时，TVSDK将调度播放事件TimelineEvent。[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED)。

| 事件 | 意义 |
|---|---|
| AdBreakPlaybackEvent。[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | 广告中断已经完全播放。 |
| AdBreakPlaybackEvent。[AD_BREAK_BRICKPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | 在播放过程中跳过广告中断。 |
| AdBreakPlaybackEvent。[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | 广告中断已开始。 |
| AdClickEvent。[广告单击(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | 用户已点击该广告。 向应用程序提供有关用户点击的广告的信息，以响应应用程序对`MediaPlayerView`的`notifyClick`调用。 |
| AdPlaybackEvent。[广告完成(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | 广告播放完整。 |
| AdPlaybackEvent。[广告进度(_P)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | 广告播放已进行。 在广告播放时多次调度。 |
| AdPlaybackEvent。[广告搜寻(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 跨广告边界或广告内发生搜索。 |
| AdPlaybackEvent。[广告开始(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 广告已开始。 |