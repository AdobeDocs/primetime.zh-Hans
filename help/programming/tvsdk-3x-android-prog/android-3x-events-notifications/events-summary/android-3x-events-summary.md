---
description: 您的应用程序可以监视播放器中的活动以及播放器的更改状态，方法是监听TVSDK调度的事件。
title: Primetime播放器事件摘要
exl-id: 3912f140-1600-41fb-9dc4-306646b7cd85
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Primetime播放器事件摘要{#primetime-player-events-summary}

您的应用程序可以监视播放器中的活动以及播放器的更改状态，方法是监听TVSDK调度的事件。

## 事件 {#events}

TVSDK会在发生应用程序必须响应的事件时通知您。 每个事件都与一个侦听器类相对应，并且必须实现一个回调方法。

>[!TIP]
>
>事件代码是`MediaPlayerEvent`枚举的常量。

`AdBreakCompletedEventListener`

* **** 表示广告时间的播放结束。

* **要实施的回调** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **** 这意味着在播放期间跳过了广告时间。

* **要实施的回调** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **** 这意味着广告时间的播放已开始。

* **要实施的回调** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **事件代码** `AD_BREAK_START`

`AdClickedEventListener`

* **** 这表示在播放期间点击了广告。

* **要实施的回调** `onAdClicked(AdClickEvent event)`
* **事件代码** `AD_CLICK`

`AdCompletedEventListener`

* **** 表示广告播放结束。

* **要实施的回调** `onAdCompleted(AdPlaybackEvent event)`

* **事件代码** `AD_COMPLETE`

`AdProgressEventListener`

* **** MaingReporting在播放期间进度。

* **要实施的回调** `onAdProgress(AdPlaybackEvent event)`

* **事件代码** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **** MaingPrimetime广告决策广告解析结束。此事件仅适用于VOD内容。

* **要实施的回调** `onAdResolutionComplete()`

* **事件代码** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **** 这意味着广告的播放已开始。

* **要实施的回调** `onAdStarted(AdPlaybackEvent event)`

* **事件代码** `AD_START`

`AudioUpdatedEventListener`

* **** 意思已检测到新音轨。

* **要实施的回调** `onAudioUpdated(MediaPlayerItemEvent event)`

* **事件代码** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **** 这意味着播放器已开始缓冲。

* **要实施的回调** `onBufferingBegin(BufferEvent event)`

* **事件代码** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **** 这意味着播放器已停止缓冲。

* **要实施的回调** `onBufferingEnd(BufferEvent event)`

* **事件代码** `BUFFERING_END`

`BufferPreparedEventListener`

* **** 含义缓冲区已准备好。

* **要实施的回调** `onBufferPrepared()`

* **事件代码** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **** 含义检测到新字幕跟踪。

* **要实施的回调** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **事件代码** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **** 这意味着已在媒体流中检测到新的DRM元数据。

* **要实施的回调** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **事件代码** `DRM_METADATA`

`ItemCreatedEventListener`

* **** 表示已创建新的媒体播放器项目。

* **要实施的回调** `onItemCreated(MediaPlayerItemEvent event)`

* **事件代码** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **** 表示已为当前项目创建新加载信息。

* **要实施的回调** `onLoadComplete(MediaPlayerItemEvent event)`

* **事件代码** `ITEM_UPDATED`

`LoadInformationEventListener`

* **** 表示已加载新区段。

* **要实施的回调** `onLoadInformation(LoadInformationEvent event)`

* **事件代码** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **** 含义主清单或播放列表已更新。

* **要实施的回调** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **事件代码** `MANIFEST_UPDATED`

`NotificationEventListener`

* **** 表示操作失败。

* **要实施的回调** `onNotification(NotificationEvent event)`

* **事件代码** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **** 这意味着播放范围已更新。

* **要实施的回调** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **事件代码** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **** 这意味着屏幕上会显示新的播放率。

* **要实施的回调** `onRatePlaying(PlaybackRateEvent event)`

* **事件代码** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **** 表示已设置MediaPlayer的速率属性。

* **要实施的回调** `onRateSelected(PlaybackRateEvent event)`

* **事件代码** `RATE_SELECTED`

`PlayStartEventListener`

* **** 表示播放已开始。

* **要实施的回调** `onPlayStart()`

* **事件代码** `PLAY_START`

`ProfileChangeEventListener`

* **** 表示MediaPlayer的当前配置文件已更改。

* **要实施的回调** `onProfileChanged(ProfileEvent event)`

* **事件代码** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **** MaingPlayback达到时间轴保留。

* **要实施的回调** `onReservationReached(ReservationEvent event)`

* **事件代码** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **** MeasingSeek操作已启动。

* **要实施的回调** `onSeekBegin(SeekEvent event)`

* **事件代码** `SEEK_BEGIN`

`SeekEndEventListener`

* **** 含义搜寻操作已完成。

* **要实施的回调** `onSeekEnd(SeekEvent event)`

* **事件代码** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **** 含义由于内部播放规则或外部业务规则，搜寻位置已进行调整。

* **要实施的回调** `onPositionAdjusted(SeekEvent event)`

* **事件代码** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **** 表示可用媒体的大小。

* **要实施的回调** `onSizeAvailable(SizeAvailableEvent event)`

* **事件代码** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **** 表示MediaPlayer状态已更改。

* **要实施的回调** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **事件代码** `STATUS_CHANGED`

`TimeChangeEventListener`

* **** 含义播放头已更改。

* **要实施的回调** `onTimeChanged(TimeChangeEvent event)`

* **事件代码** `TIME_CHANGED`

`TimedEventEventListener`

* **** 含义操作已完成，且所用的时间为操作。

* **要实施的回调** `onTimedEvent(TimedEventEvent event)`

* **事件代码** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **** 这意味着已将新的定时元数据添加到后台的项目。

* **要实施的回调** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代码** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **** 这意味着在媒体流中检测到新的定时元数据。

* **要实施的回调** `onTimedMetadata(TimedMetadataEvent event)`

* **事件代码** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **** 含义时间轴已修改。可能已在时间轴中添加或删除了广告。

* **要实施的回调** `onTimelineUpdated(TimelineEvent event)`

* **事件代码** `TIMELINE_UPDATED`
