---
description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下禁用延迟广告解析）。
keywords: 延迟；广告解析；广告加载；延迟加载
title: 启用延迟广告解决
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# 启用延迟广告解析{#enable-lazy-ad-resolving}

您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下禁用延迟广告解析）。

可以通过调用[AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-)（为true或false）来启用或禁用“延迟广告解析”。

* 使用AdvertisingMetadata中的布尔&#x200B;*hasDelayAdLoading*&#x200B;和&#x200B;*setDelayAdLoading*&#x200B;方法控制广告分辨时间以及时间轴上广告的放置：

   * 如果&#x200B;*hasDelayAdLoading*&#x200B;返回false，则TVSDK会等到所有广告都解析并置入后，再转换到PREPARED状态。
   * 如果&#x200B;*hasDelayAdLoading*&#x200B;返回true，则TVSDK仅将初始广告和过渡解析为PREPARED状态。

      * 其余广告在播放过程中进行解析和放置。
   * 当*hasPreroll *或&#x200B;*hasLivePreroll*&#x200B;返回false时，TVSDK假定不存在预卷广告并立即开始内容的播放。 这些值默认为true。


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

要将广告准确反映为拖拽栏上的提示，请倾听`TimelineEvent`事件，并在每次收到此事件时重绘拖拽栏。

如果为VOD流启用了“延迟广告解析”，则所有广告分段都会放在时间轴上，但是，许多广告分段仍无法解析。 应用程序可以通过检查`TimelineMarker::getDuration()`来确定是否绘制这些标记。 如果该值大于零，则广告分段内的广告已解析。

TVSDK在解决广告中断时以及当播放器过渡为PREPARED状态时分派此事件。

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
