---
description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下，“延迟广告解析”处于启用状态）。
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下，“延迟广告解析”处于启用状态）。
seo-title: 启用延迟广告解决
title: 启用延迟广告解决
uuid: a084ee0b-53af-4600-91f6-d30ccc89699d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 启用延迟广告解决 {#enable-lazy-ad-resolving}

您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下，“延迟广告解析”处于启用状态）。

您可以通过调用AdvertisingMetadata.setDelayLoading（或）来启用或 [禁用延迟广告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) 解析 `true``false`。

1. 使用中的 `hasDelayAdLoading` 布尔 `setDelayAdLoading` 和方 `AdvertisingMetadata` 法控制广告分辨时间和广告在时间轴上的位置：

   * 如果 `hasDelayAdLoading` 返回false，则TVSDK会等到所有广告都得到解析和放置后，再转换到PREPARED状态。
   * 如果 `hasDelayAdLoading` 返回true，则TVSDK仅解析初始广告和到PREPARED状态的过渡。 在播放过程中，将解析和放置其余广告。
   * 当 `hasPreroll` 或返 `hasLivePreroll` 回false时，TVSDK假定没有预卷广告并立即开始播放内容。 这些默认值为true。

      与延迟广告解析相关的API:

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

1. 要将广告准确地反映为滑动条上的提示，请侦听该事 `TimelineEvent` 件，并在您每次收到该事件时重绘滑动条。

   当为VOD流启用“延迟广告解析”时，并非当您的播放器进入PREPARED状态时，所有广告都会放在时间轴上，因此您的播放器必须显式重绘划动条。

   TVSDK会优化此事件的调度，以最大限度地减少您必须重绘划动条的次数；因此，时间轴事件的数量与要放置在时间轴上的广告分段数无关。 例如，如果您有五个广告中断，则可能不会收到五个事件。

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

>要验证延迟广告解析功能是启用还是禁用，请调用 `AdvertisingMetadata.hasDelayAdLoading`。 返回值表示 `true` 已启用“延迟广告解析”;表 `false` 示功能被禁用。

