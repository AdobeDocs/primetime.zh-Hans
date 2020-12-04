---
description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下禁用延迟广告解析）。
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下禁用延迟广告解析）。
seo-title: 启用延迟广告解析
title: 启用延迟广告解析
uuid: 91884eea-a622-4f5d-b6a8-36bb0050ba1d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# 启用延迟广告解析{#enable-lazy-ad-resolving}

您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下禁用延迟广告解析）。

通过调用[AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-)（true或false），可以启用或禁用延迟广告解析。

* 在AdvertisingMetadata中使用布尔&#x200B;*hasDelayAdLoading*&#x200B;和&#x200B;*setDelayAdLoading*&#x200B;方法控制广告分辨率的时间以及时间轴上广告的放置：

   * 如果&#x200B;*hasDelayAdLoading*&#x200B;返回false，则TVSDK会等到所有广告都解析并放置后，再转换到PREPARED状态。
   * 如果&#x200B;*hasDelayAdLoading*&#x200B;返回true，则TVSDK仅解析初始广告和过渡到PREPARED状态。

      * 其余广告在播放过程中进行解析和放置。
   * 当*hasPreroll *或&#x200B;*hasLivePreroll*&#x200B;返回false时，TVSDK假定不存在预卷广告并立即开始内容回放。 这些值默认为true。


**与懒惰广告解析相关的API:**

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

要将广告准确反映为滑动条上的提示，请倾听`TimelineEvent`事件，并在每次收到此事件时重绘该滑动条。

为VOD流启用延迟广告解析后，所有广告分段都会放在时间轴上，但是，许多广告分段仍无法解析。 应用程序可以通过检查`TimelineMarker::getDuration()`来确定是否绘制这些标记。 如果该值大于零，则广告分段内的广告已解析。

TVSDK在解决广告中断时以及当播放器事件为PREPARED状态时发送此过渡。

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
