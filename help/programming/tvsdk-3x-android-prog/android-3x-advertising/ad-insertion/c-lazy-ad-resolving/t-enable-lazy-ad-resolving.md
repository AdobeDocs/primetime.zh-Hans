---
description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下禁用延迟广告解析）。
keywords: 延迟；广告解析；广告加载；延迟加载
title: 启用延迟广告解析
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# 启用延迟广告解析 {#enable-lazy-ad-resolving}

您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下禁用延迟广告解析）。

您可以通过调用来启用或禁用延迟广告解析 [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) 为true或false。

* 使用布尔值 *hasDelayAdLoading* 和 *setDelayAdLoading* AdvertisingMetadata中用于控制广告解析时间和广告在时间轴上的投放的方法：

   * 如果 *hasDelayAdLoading* 返回false，TVSDK将等待所有广告解析并放置之后再过渡到“已准备”状态。
   * 如果 *hasDelayAdLoading* 返回true，TVSDK仅解析初始广告和过渡到“已准备”状态。

      * 剩余的广告将在播放期间解析并置入。

   * 当*hasPreroll *或 *hasLivePreroll* return false， TVSDK假定没有前置广告，并立即开始播放内容。 这些参数默认设置为true。

**与延迟广告解析相关的API：**

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

要在搓擦条上准确地将广告反映为提示，请聆听 `TimelineEvent`事件，并在每次收到此事件时重绘搓擦条。

为VOD流启用延迟广告解析后，所有广告时间都会放在时间轴上，但是，许多广告时间尚未解析。 应用程序可以通过检查 `TimelineMarker::getDuration()`. 如果该值大于零，则表示已解析广告时间内的广告。

TVSDK会在广告时间解决后，以及在播放器过渡到“已准备”状态时调度此事件。

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
