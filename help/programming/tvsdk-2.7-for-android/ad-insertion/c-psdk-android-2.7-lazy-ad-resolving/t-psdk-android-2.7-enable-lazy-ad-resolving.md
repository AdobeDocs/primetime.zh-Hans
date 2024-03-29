---
description: 您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下启用延迟广告解析）。
keywords: 延迟；广告解析；广告加载；延迟加载
title: 启用延迟广告解析
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 启用延迟广告解析 {#enable-lazy-ad-resolving}

您可以使用现有的延迟广告加载机制启用或禁用延迟广告解析功能（默认情况下启用延迟广告解析）。

您可以通过调用来启用或禁用延迟广告解析 [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) 替换为 `true` 或 `false`.

1. 使用布尔值 `hasDelayAdLoading` 和 `setDelayAdLoading` 中的方法 `AdvertisingMetadata` 要控制广告分辨时间和广告在时间轴上的放置，请执行以下操作：

   * 如果 `hasDelayAdLoading` 返回false，TVSDK将等待所有广告解析并放置之后再过渡到“已准备”状态。
   * 如果 `hasDelayAdLoading` 返回true，TVSDK仅解析初始广告和过渡到“已准备”状态。 剩余的广告将在播放期间解析并置入。
   * 时间 `hasPreroll` 或 `hasLivePreroll` return false， TVSDK假定没有前置广告，并立即开始播放内容。 这些参数默认为true。

     与延迟广告解析相关的API：

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

1. 要在搓擦条上准确地将广告反映为提示，请聆听 `TimelineEvent` 事件，并在每次收到此事件时重绘搓擦条。

   为VOD流启用延迟广告解析后，当播放器进入“已准备”状态时，并非所有广告都会放在时间轴上，因此播放器必须明确重新绘制推移栏。

   TVSDK将优化此事件的发送，以最大限度地减少必须重新绘制推移栏的次数；因此，时间线事件的数量与要放置在时间线上的广告时间数无关。 例如，如果您有五个广告时间，则可能不会正好收到五个事件。

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

>要验证是否启用或禁用延迟广告解析功能，请调用 `AdvertisingMetadata.hasDelayAdLoading`. 返回值 `true` 意味着已启用延迟广告解析； `false` 表示该功能已禁用。
