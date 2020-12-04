---
description: 这些类描述TVSDK为响应各种事件而向媒体播放器发送的活动。
seo-description: 这些类描述TVSDK为响应各种事件而向媒体播放器发送的活动。
seo-title: 事件类
title: 事件类
uuid: 5e63d43c-6112-4958-b8cd-ccf123affd08
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# 事件类{#events-classes}

这些类描述TVSDK为响应各种事件而向媒体播放器发送的活动。

包：[com.adobe.mediacore.事件](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| 名称 | 意义 |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | 课。 广告中断开始或结束。 |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | 课。 用户点击了广告。 |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | 课。 玩家播放了广告。 |
| [BufferEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | 课。 播放器开始或停止缓冲。 |
| [CustomAdEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/CustomAdEvent.html) | 课。 播放器显示自定义广告加载状态，并可忽略有错误或加载时间过长的广告。 |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | 课。 新的DRM元数据与当前项目相关联。 |
| [LoadInformationEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | 课。 下载信息可用于当前正在播放的媒体流。 |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | 课。 已创建媒体播放器项。 |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | 课。 加载操作已完成。 由`MediaPlayerItemLoader`调度以通知其客户端。 |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | 课。 媒体播放器状态已更改。 |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | 课。 单击`MediaPlayerView`。 |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | 课。 媒体播放器的播放速率会发生变化。 |
| [ProfileEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | 课。 由于网络或机器条件，媒体播放器的自适应比特率切换算法已切换到另一个用户档案。 |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | 课。 播放器开始搜索或搜索操作已完成。 |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | 课。 视频大小可用。 |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | 课。 媒体播放器的状态已更改。 |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | 课。 时间元数据由机会检测器处理。 |
| [时间轴事件](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | 课。 媒体播放器时间轴已更改。 |