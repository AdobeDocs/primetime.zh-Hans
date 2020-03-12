---
description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下，延迟广告解析处于禁用状态）。
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下，延迟广告解析处于禁用状态）。
seo-title: 启用延迟广告解决
title: 启用延迟广告解决
uuid: 91884eea-a622-4f5d-b6a8-36bb0050ba1d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 启用延迟广告解决 {#enable-lazy-ad-resolving}

您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下，延迟广告解析处于禁用状态）。

通过调用AdvertisingMetadata.setDelayLoading（true或false），可 [以启用或禁用“延迟广告解析](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) ”。

* 使用AdvertisingMetadata中 *的Boolean hasDelayAdLoading* 和 *setDelayAdLoading* 方法控制广告分辨时间和广告在时间轴上的放置：

   * 如果 *hasDelayAdLoading返回false* ，则TVSDK会等到所有广告都解析并放置完毕后，再转换到PREPARED状态。
   * 如果 *hasDelayAdLoading返回true* ，则TVSDK仅解析初始广告和到PREPARED状态的过渡。

      * 在播放过程中，将解析和放置其余广告。
   * 当*hasPreroll *或 *hasLivePreroll* 返回false时，TVSDK假定没有预卷广告并立即开始播放内容。 这些值默认为true。


**与延迟广告解析相关的API:**

```
Class:    com.adobe.mediacore.metadata.AdvertisingMetadata 
Methods: 
    public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
    public final void setDelayAdLoading() // Enable or disable Lazy Ad Resolving 
    public final void setDelayAdLoadingTolerance() // Sets the Lazy Ad Resolving Tolerance level.  This value is added to the BufferControlParameters::playBufferTime and the content's EXT-X-TARGETDURATION to determine when ad breaks should resolve 
    public final double getDelayAdLoadingTolerance() // Gets the Lazy Ad Resolving Tolerance level 
    public final boolean hasPreroll() // Check for existence of pre-roll ads 
    public final void setPreroll() // Set pre-roll true or false 
    public final boolean hasLivePreroll() // Check for live pre-roll ads 
    public final void setLivePreroll() // Set live pre-roll true or false

Class:     com.adobe.mediacore.timeline.TimelineMarker 
Methods: 
    public double getDuration() // Returns the current duration of the TimelineMarker.  This will be zero if the ad break has not yet resolved. 
    public Placement.Type getPlacementType() // Returns whether
```

要将广告准确地反映为滑动条上的提示，请侦听该 `TimelineEvent`事件，并在每次收到该事件时重绘滑动条。

当为VOD流启用“延迟广告解析”时，所有广告分段将放在时间轴上，但是，许多广告分段尚未解析。 应用程序可以通过检查来确定是否绘制这些标记 `TimelineMarker::getDuration()`。 如果该值大于零，则广告分时段内的广告已解析。

TVSDK在解决广告中断时以及播放器转换到PREPARED状态时调度此事件。

```
mediaPlayer.addEventListener(MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
/** 
* ... 
*/ 
public void onTimelineUpdated(TimelineEvent event) { 
for (PlaybackManagerEventListener listener : eventListeners) { 
  listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
}
```
