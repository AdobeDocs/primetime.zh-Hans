---
description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下启用延迟广告解析）。
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下启用延迟广告解析）。
seo-title: 启用延迟广告解析
title: 启用延迟广告解析
uuid: a084ee0b-53af-4600-91f6-d30ccc89699d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 启用延迟广告解析{#enable-lazy-ad-resolving}

您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下启用延迟广告解析）。

可以通过调用[AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-)（带有`true`或`false`）来启用或禁用延迟广告解析。

1. 使用`AdvertisingMetadata`中的布尔`hasDelayAdLoading`和`setDelayAdLoading`方法控制广告分辨时间以及时间轴上广告的位置：

   * 如果`hasDelayAdLoading`返回false，则TVSDK会等到所有广告都解析并放置后，再转换为PREPARED状态。
   * 如果`hasDelayAdLoading`返回true，则TVSDK仅将初始广告和过渡解析为PREPARED状态。 其余广告在播放过程中进行解析和放置。
   * 当`hasPreroll`或`hasLivePreroll`返回false时，TVSDK假定不存在预卷广告并立即开始内容的播放。 这些默认值为true。

      与懒惰广告解析相关的API:

      ```
      Class: 
         com.adobe.mediacore.metadata.AdvertisingMetadata 
      
      Methods: 
      […] 
          public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
          public final void setDelayAdLoading()    // Enable or disable Lazy Ad Resolving 
          public final boolean hasPreroll()        // Check for existence of pre-roll ads 
          public final void setPreroll()           // Set pre-roll true or false 
          public final boolean hasLivePreroll()    // Check for live pre-roll ads 
          public final void setLivePreroll()       // Set live pre-roll true or false 
      […]
      ```

1. 要将广告准确反映为滑动条上的提示，请倾听`TimelineEvent`事件，并在每次收到此事件时重绘该滑动条。

   当为VOD流启用延迟广告解析时，当播放器进入PREPARED状态时，并非所有广告都放在时间轴上，因此播放器必须显式重绘划动条。

   TVSDK会优化此事件的派单，以最大限度地减少您重绘拖拽条的次数；因此，时间轴事件的数量与要放置在时间轴上的广告分段数无关。 例如，如果您有五个广告中断，您可能不会收到五个事件。

   ```java
   mediaPlayer.addEventListener 
       (MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
   /** 
    * ... 
    */ 
   public void onTimelineUpdated(TimelineEvent event) { 
   
       for (PlaybackManagerEventListener listener : eventListeners) { 
           listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
       } 
   } 
   ```

>要验证延迟广告解析功能是启用还是禁用，请调用`AdvertisingMetadata.hasDelayAdLoading`。 返回值`true`表示已启用“延迟广告解析”;`false`表示功能已禁用。

