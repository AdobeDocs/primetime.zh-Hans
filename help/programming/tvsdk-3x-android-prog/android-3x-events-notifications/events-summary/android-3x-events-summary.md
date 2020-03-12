---
description: 您的应用程序可以监视播放器中的活动，以及播放器状态的变化，方法是侦听TVSDK调度的事件。
seo-description: 您的应用程序可以监视播放器中的活动，以及播放器状态的变化，方法是侦听TVSDK调度的事件。
seo-title: Primetime播放器活动摘要
title: Primetime播放器活动摘要
uuid: b2ff74f2-c373-42da-a717-2f0550cbcb7f
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Primetime播放器活动摘要 {#primetime-player-events-summary}

您的应用程序可以监视播放器中的活动，以及播放器状态的变化，方法是侦听TVSDK调度的事件。

## 活动 {#events}

TVSDK会在应用程序必须响应的事件发生时通知您。 每个事件都对应一个监听器类，并且有一个必须实现的回调方法。

>[!TIP]
>
>事件代码是枚举的常 `MediaPlayerEvent` 数。

`AdBreakCompletedEventListener`

* **这意味着** ，广告中断的播放已完成。

* **要实现的回调**`onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **活动代码**`AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **这意味着** ，在播放过程中，广告中断被跳过。

* **要实现的回调**`onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **活动代码**`AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **这意味着** ，广告中断的播放已开始。

* **要实现的回调**`onAdBreakStarted(AdBreakPlaybackEvent event)`

* **活动代码**`AD_BREAK_START`

`AdClickedEventListener`

* **这意味着** ，在播放过程中单击了广告。

* **要实现的回调**`onAdClicked(AdClickEvent event)`
* **活动代码**`AD_CLICK`

`AdCompletedEventListener`

* **这意味着** ，广告的播放已完成。

* **要实现的回调**`onAdCompleted(AdPlaybackEvent event)`

* **活动代码**`AD_COMPLETE`

`AdProgressEventListener`

* **意味着** “在播放期间报告进度”。

* **要实现的回调**`onAdProgress(AdPlaybackEvent event)`

* **活动代码**`AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **这意味着** Primetime广告决策和解决方案已完成。 此活动仅适用于VOD内容。

* **要实现的回调**`onAdResolutionComplete()`

* **活动代码**`AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **这意味着** ，广告的播放已开始。

* **要实现的回调**`onAdStarted(AdPlaybackEvent event)`

* **活动代码**`AD_START`

`AudioUpdatedEventListener`

* **这意味着** ，已检测到新的音轨。

* **要实现的回调**`onAudioUpdated(MediaPlayerItemEvent event)`

* **活动代码**`AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **这意味着** ，播放器已开始缓冲。

* **要实现的回调**`onBufferingBegin(BufferEvent event)`

* **活动代码**`BUFFERING_BEGIN`

`BufferingEndEventListener`

* **这意味着** ，播放器已停止缓冲。

* **要实现的回调**`onBufferingEnd(BufferEvent event)`

* **活动代码**`BUFFERING_END`

`BufferPreparedEventListener&quot;

* **意思** ：缓冲区已准备好。

* **要实现的回调**`onBufferPrepared()`

* **活动代码**`BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **这意味着** ，已检测到新的字幕轨道。

* **要实现的回调**`onCaptionsUpdated(MediaPlayerItemEvent event)`

* **活动代码**`CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **这意味着** ，在媒体流中检测到新的DRM元数据。

* **要实现的回调**`onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **活动代码**`DRM_METADATA`

`ItemCreatedEventListener`

* **这意味着** ，新的媒体播放器项目已创建。

* **要实现的回调**`onItemCreated(MediaPlayerItemEvent event)`

* **活动代码**`ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **这意味着** ，已为当前项目创建新的加载信息。

* **要实现的回调**`onLoadComplete(MediaPlayerItemEvent event)`

* **活动代码**`ITEM_UPDATED`

`LoadInformationEventListener`

* **这意味着** ，新区段已加载。

* **要实现的回调**`onLoadInformation(LoadInformationEvent event)`

* **活动代码**`LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **这意味着** ，主清单或播放列表已更新。

* **要实现的回调**`onMainManifestUpdated(MediaPlayerItemEvent event)`

* **活动代码**`MANIFEST_UPDATED`

`NotificationEventListener`

* **这意味着** ，操作已失败。

* **要实现的回调**`onNotification(NotificationEvent event)`

* **活动代码**`OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **这意味着** ，播放范围已更新。

* **要实现的回调**`onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **活动代码**`PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **这意味着** ，新的播放速率在屏幕上可见。

* **要实现的回调**`onRatePlaying(PlaybackRateEvent event)`

* **活动代码**`RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **这意味着** MediaPlayer的rate属性已设置。

* **要实现的回调**`onRateSelected(PlaybackRateEvent event)`

* **活动代码**`RATE_SELECTED`

`PlayStartEventListener`

* **这意味着** ，播放已开始。

* **要实现的回调**`onPlayStart()`

* **活动代码**`PLAY_START`

`ProfileChangeEventListener`

* **这意味着** MediaPlayer的当前配置文件已更改。

* **要实现的回调**`onProfileChanged(ProfileEvent event)`

* **活动代码**`PROFILE_CHANGED`

`ReservationReachedEventListener`

* **这意味着** “播放”达到时间轴保留。

* **要实现的回调**`onReservationReached(ReservationEvent event)`

* **活动代码**`RESERVATION_REACHED`

`SeekBeginEventListener`

* **这意味着** “搜索”操作已开始。

* **要实现的回调**`onSeekBegin(SeekEvent event)`

* **活动代码**`SEEK_BEGIN`

`SeekEndEventListener`

* **这意味着** ，搜索操作已完成。

* **要实现的回调**`onSeekEnd(SeekEvent event)`

* **活动代码**`SEEK_END`

`SeekPositionAdjustedEventListener`

* **这意味着** ，搜索位置已因内部播放规则或外部业务规则而调整。

* **要实现的回调**`onPositionAdjusted(SeekEvent event)`

* **活动代码**`SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **这意味着** ，介质的大小可用。

* **要实现的回调**`onSizeAvailable(SizeAvailableEvent event)`

* **活动代码**`SIZE_AVAILABLE`

`StatusChangeEventListener`

* **这意味着** MediaPlayer状态已更改。

* **要实现的回调**`onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **活动代码**`STATUS_CHANGED`

`TimeChangeEventListener`

* **这意味着** ，播放头已更改。

* **要实现的回调**`onTimeChanged(TimeChangeEvent event)`

* **活动代码**`TIME_CHANGED`

`TimedEventEventListener`

* **意思** ：此操作完成时，需要花费的时间。

* **要实现的回调**`onTimedEvent(TimedEventEvent event)`

* **活动代码**`TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **这意味着** ，新的定时元数据已添加到后台项目。

* **要实现的回调**`onTimedMetadata(TimedMetadataEvent event)`

* **活动代码**`TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **这意味着** ，在媒体流中检测到新的定时元数据。

* **要实现的回调**`onTimedMetadata(TimedMetadataEvent event)`

* **活动代码**`TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **这意味着** ，时间轴已被修改。 广告可能已添加到时间轴中或从时间轴中删除。

* **要实现的回调**`onTimelineUpdated(TimelineEvent event)`

* **活动代码**`TIMELINE_UPDATED`