---
description: TVSDK会根据广告相关操作（如广告开始播放时）调度广告播放事件。
seo-description: TVSDK会根据广告相关操作（如广告开始播放时）调度广告播放事件。
seo-title: 广告播放事件
title: 广告播放事件
uuid: 63138237-2315-45ff-914d-369da18fdff7
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 广告播放事件 {#ad-playback-events}

TVSDK会根据广告相关操作（如广告开始播放时）调度广告播放事件。

要获得有关所有广告播放相关事件的通知，请向以下事件的对象 `MediaPlayer` 注册监听器。

>[!TIP]
>
>当广告插入媒体或从媒体中删除广告时，TVSDK将调度播放事件TimelineEvent。[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED)。

| 活动 | 意义 |
|---|---|
| AdBreakPlaybackEvent。[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | 广告中断已经完全演奏。 |
| AdBreakPlaybackEvent。[AD_BREAK_BRIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | 在播放过程中跳过了广告中断。 |
| AdBreakPlaybackEvent。[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | 广告中断已开始。 |
| AdClickEvent。[广告单击(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | 用户已点击该广告。 向应用程序提供有关用户点击的广告的信息，以响应应用程序对的 `notifyClick` 调用 `MediaPlayerView`。 |
| AdPlaybackEvent。[AD_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | 广告已完全播放。 |
| AdPlaybackEvent。[广告进度(_P)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | 广告播放已进行。 播放广告时多次调度。 |
| AdPlaybackEvent。[AD_SEEK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 在广告边界或广告内发生搜索。 |
| AdPlaybackEvent。[AD STARTED(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 广告已开始。 |