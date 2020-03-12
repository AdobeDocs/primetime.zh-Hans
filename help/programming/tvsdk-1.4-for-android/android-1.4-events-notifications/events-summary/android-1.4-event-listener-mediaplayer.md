---
description: TVSDK会根据广告相关操作（如广告开始播放时）调度广告播放事件。
seo-description: TVSDK会根据广告相关操作（如广告开始播放时）调度广告播放事件。
seo-title: 广告播放事件
title: 广告播放事件
uuid: dd6991ae-3e33-4d92-92e9-26b1086a555a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 广告播放事件{#ad-playback-events}

TVSDK会根据广告相关操作（如广告开始播放时）调度广告播放事件。

要获得有关所有广告播放相关事件的通知，请注册以下回 `MediaPlayer.AdPlaybackEventListener` 调的实施。

>[!TIP]
>
>当广告插入媒体或从媒体中删除广告时，TVSDK将调度 [onTimelineUpdated播放事件](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated())。

| 活动 | 意义 |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 广告中断已经完全演奏。 |
| onAdBreakKbipted | 在播放过程中跳过了广告中断。 |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | 广告中断已开始。 |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak、Ad ad、AdClick adClick) | 用户已点击该广告。 向应用程序提供有关用户点击的广告的信息，以响应应用程序对的 `notifyClick` 调用 `MediaPlayerView`。 |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak、Ad ad) | 广告已完全播放。 |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) （AdBreak adBreak，广告，整数百分比） | 广告播放已进行。 播放广告时多次调度。 |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak、Ad ad) | 广告已开始。 |