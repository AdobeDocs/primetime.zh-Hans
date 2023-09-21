---
description: TVSDK调度广告播放事件以响应与广告相关的操作，例如当广告开始播放时。
title: 广告播放事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 广告播放事件{#ad-playback-events}

TVSDK调度广告播放事件以响应与广告相关的操作，例如当广告开始播放时。

要收到有关所有广告播放相关事件的通知，请注册以下实施 `MediaPlayer.AdPlaybackEventListener` 包括以下回调。

>[!TIP]
>
>当广告插入媒体或从媒体中删除时，TVSDK会调度播放事件 [时间线已更新](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| 事件 | 含义 |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 广告时间已完全播放。 |
| onAdBreakSkipped | 播放期间跳过了一个广告时间。 |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 广告时间已开始。 |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) （AdBreak adBreak、广告、AdClick adClick） | 用户已单击广告。 向应用程序提供有关用户点击的广告的信息，以响应您的应用程序调用 `notifyClick` 在 `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) （AdBreak adBreak、广告） | 广告已播放完毕。 |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) （AdBreak adBreak、广告广告、整型百分比） | 广告播放已取得进展。 在广告播放时多次调度。 |
| [Adstart上的](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) （AdBreak adBreak、广告） | 广告已开始。 |
