---
description: 这些类描述TVSDK向媒体播放器调度以响应各种活动的事件。
title: 事件类
exl-id: a349984a-5e47-4895-a56f-ef25eb372c79
source-git-commit: 776d3d1668f063f1595bd3ecb53603171905014a
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 事件类 {#events-classes}

这些类描述TVSDK向媒体播放器调度以响应各种活动的事件。

包： [com.adobe.mediacore.events](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| 名称 | 含义 |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | 班级。 广告时间开始或结束。 |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | 班级。 用户单击了广告。 |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | 班级。 播放器播放了一个广告。 |
| [缓冲事件](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | 班级。 播放器已开始或停止缓冲。 |
| [CustomAdEvent](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-1-4-for-desktop-hls/advertising/custom-ads/r-psdk-dhls-1.4-custom-ad-events.html?lang=en) | 班级。 播放器会显示自定义广告加载状态，并且可以忽略有错误或加载时间过长的广告。 |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | 班级。 新的DRM元数据与当前项目相关联。 |
| [loadinformevent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | 班级。 下载信息适用于正在播放的当前媒体流。 |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | 班级。 已创建媒体播放器项目。 |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | 班级。 加载操作已完成。 分派人 `MediaPlayerItemLoader` 通知其客户端。 |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | 班级。 媒体播放器状态已更改。 |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | 班级。 此 `MediaPlayerView` 已单击。 |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | 班级。 媒体播放器的播放速率发生更改。 |
| [配置文件事件](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | 班级。 由于网络或机器条件，媒体播放器的自适应比特率切换算法已切换到另一个配置文件。 |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | 班级。 播放器开始进行搜寻或搜寻操作已完成。 |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | 班级。 视频大小可用。 |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | 班级。 媒体播放器的状态已更改。 |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | 班级。 机会检测器处理定时元数据。 |
| [时间线事件](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | 班级。 媒体播放器时间轴已更改。 |
