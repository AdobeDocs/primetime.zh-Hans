---
description: TVSDK调度广告播放事件以响应与广告相关的操作，例如当广告开始播放时。
title: 广告播放事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 广告播放事件 {#ad-playback-events}

TVSDK调度广告播放事件以响应与广告相关的操作，例如当广告开始播放时。

要收到有关所有广告播放相关事件的通知，请在注册侦听器 `MediaPlayer` 对象。

>[!TIP]
>
>当广告插入媒体或从媒体中删除时，TVSDK会调度播放事件TimelineEvent。[时间线已更新](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| 事件 | 含义 |
|---|---|
| AdBreakPlaybackEvent。[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | 广告时间已完全播放。 |
| AdBreakPlaybackEvent。[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | 播放期间跳过了一个广告时间。 |
| AdBreakPlaybackEvent。[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | 广告时间已开始。 |
| AdClickEvent。[添加点击(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | 用户已单击广告。 向应用程序提供有关用户点击的广告的信息，以响应您的应用程序调用 `notifyClick` 在 `MediaPlayerView`. |
| AdPlaybackEvent。[AD已完成(_C)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | 广告已播放完毕。 |
| AdPlaybackEvent。[广告进度(_P)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | 广告播放已取得进展。 在广告播放时多次调度。 |
| AdPlaybackEvent。[AD_SEEK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 搜寻已跨广告边界或广告内发生。 |
| AdPlaybackEvent。[广告开始(_S)](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | 广告已开始。 |
