---
description: 您的应用程序可以通过侦听由TVSDK调度的事件，监控播放器中的活动和播放器状态的变化。
title: Primetime播放器事件摘要
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Primetime播放器事件摘要 {#primetime-player-events-summary}

您的应用程序可以通过侦听由TVSDK调度的事件，监控播放器中的活动和播放器状态的变化。

## 活动 {#events}

TVSDK会在发生应用程序必须响应的事件时通知您。 每个事件都对应一个监听程序类，其中包含必须实现的回调方法。

>[!TIP]
>
>事件代码是 `MediaPlayerEvent` 枚举。

`AdBreakCompletedEventListener`

* **含义** 广告时间的播放结束。

* **要实施的回调** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **含义** 播放期间跳过了一个广告时间。

* **要实施的回调** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **含义** 广告时间的播放已开始。

* **要实施的回调** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_START`

`AdClickedEventListener`

* **含义** 在播放期间点击了广告。

* **要实施的回调** `onAdClicked(AdClickEvent event)`
* **事件代码** `AD_CLICK`

`AdCompletedEventListener`

* **含义** 广告播放结束。

* **要实施的回调** `onAdCompleted(AdPlaybackEvent event)`

* **事件代码** `AD_COMPLETE`

`AdProgressEventListener`

* **含义** 报告播放期间的进度。

* **要实施的回调** `onAdProgress(AdPlaybackEvent event)`

* **事件代码** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **含义** Primetime ad decisioningad解析已完成。 此事件仅适用于VOD内容。

* **要实施的回调** `onAdResolutionComplete()`

* **事件代码** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **含义** 广告的播放已开始。

* **要实施的回调** `onAdStarted(AdPlaybackEvent event)`

* **事件代码** `AD_START`

`AudioUpdatedEventListener`

* **含义** 已检测到新的音轨。

* **要实施的回调** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代码** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **含义** 播放器已开始缓冲。

* **要实施的回调** `onBufferingBegin(BufferEvent event)`

* **事件代码** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **含义** 播放器已停止缓冲。

* **要实施的回调** `onBufferingEnd(BufferEvent event)`

* **事件代码** `BUFFERING_END`

`BufferPreparedEventListener`

* **含义** 已准备缓冲区。

* **要实施的回调** `onBufferPrepared()`

* **事件代码** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **含义** 已检测到新的描述跟踪。

* **要实施的回调** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代码** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **含义** 已在媒体流中检测到新的DRM元数据。

* **要实施的回调** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代码** `DRM_METADATA`

`ItemCreatedEventListener`

* **含义** 已创建新的媒体播放器项目。

* **要实施的回调** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代码** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **含义** 已为当前项目创建新的加载信息。

* **要实施的回调** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代码** `ITEM_UPDATED`

`LoadInformationEventListener`

* **含义** 已加载新区段。

* **要实施的回调** `onLoadInformation(LoadInformationEvent event)`

* **事件代码** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **含义** 主清单或播放列表已更新。

* **要实施的回调** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代码** `MANIFEST_UPDATED`

`NotificationEventListener`

* **含义** 操作失败。

* **要实施的回调** `onNotification(NotificationEvent event)`

* **事件代码** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **含义** 已更新播放范围。

* **要实施的回调** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代码** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **含义** 屏幕上会显示新的播放速率。

* **要实施的回调** `onRatePlaying(PlaybackRateEvent event)`

* **事件代码** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **含义** 已设置MediaPlayer的rate属性。

* **要实施的回调** `onRateSelected(PlaybackRateEvent event)`

* **事件代码** `RATE_SELECTED`

`PlayStartEventListener`

* **含义** 已开始播放。

* **要实施的回调** `onPlayStart()`

* **事件代码** `PLAY_START`

`ProfileChangeEventListener`

* **含义** MediaPlayer的当前配置文件已更改。

* **要实施的回调** `onProfileChanged(ProfileEvent event)`

* **事件代码** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **含义** 播放已达到时间线保留。

* **要实施的回调** `onReservationReached(ReservationEvent event)`

* **事件代码** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **含义** 搜寻操作已开始。

* **要实施的回调** `onSeekBegin(SeekEvent event)`

* **事件代码** `SEEK_BEGIN`

`SeekEndEventListener`

* **含义** 搜寻操作已完成。

* **要实施的回调** `onSeekEnd(SeekEvent event)`

* **事件代码** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **含义** 由于内部播放规则或外部业务规则，搜寻位置已调整。

* **要实施的回调** `onPositionAdjusted(SeekEvent event)`

* **事件代码** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **含义** 介质的大小可用。

* **要实施的回调** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代码** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **含义** MediaPlayer状态已更改。

* **要实施的回调** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代码** `STATUS_CHANGED`

`TimeChangeEventListener`

* **含义** 播放头已更改。

* **要实施的回调** `onTimeChanged(TimeChangeEvent event)`

* **事件代码** `TIME_CHANGED`

`TimedEventEventListener`

* **含义** 操作已完成，且操作所用的时间也已完成。

* **要实施的回调** `onTimedEvent(TimedEventEvent event)`

* **事件代码** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **含义** 新的定时元数据已添加到后台项目。

* **要实施的回调** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代码** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **含义** 在媒体流中检测到新的定时元数据。

* **要实施的回调** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代码** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **含义** 时间线已修改。 广告可能已添加到时间轴或从时间轴中删除。

* **要实施的回调** `onTimelineUpdated(TimelineEvent event)`

* **事件代码** `TIMELINE_UPDATED`
