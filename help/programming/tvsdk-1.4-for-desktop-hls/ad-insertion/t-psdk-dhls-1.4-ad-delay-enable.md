---
description: 您可以指定是否在所有广告加载并放入时间轴中之前允许播放。 以这种方式开始播放可使查看者更快地访问主内容。 此功能仅适用于实时DVR，不适用于VOD资产等。
seo-description: 您可以指定是否在所有广告加载并放入时间轴中之前允许播放。 以这种方式开始播放可使查看者更快地访问主内容。 此功能仅适用于实时DVR，不适用于VOD资产等。
seo-title: 启用延迟广告加载
title: 启用延迟广告加载
uuid: ac7c8801-7fa2-4f17-b79c-c603b3236948
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 启用延迟广告加载{#enable-lazy-ad-loading}

您可以指定是否在所有广告加载并放入时间轴中之前允许播放。 以这种方式开始播放可使查看者更快地访问主内容。 此功能仅适用于实时DVR，不适用于VOD资产等。

1. 请使用中的Boolean `delayAdLoading` 属性 `AdvertisingMetadata`。

   * 如果为false，则TVSDK会等到所有广告都得到解析并放置后，才会转换为PREPARED状态。 默认情况下为false。
   * 如果为true，则TVSDK仅解析初始广告和转换到PREPARED状态。 在播放过程中，将解析和放置其余广告。

1. 要通过Adobe Primetime广告决策激活延迟广告加载，请在创建时将 `true` 其设置为 `AuditudeSettings`。

   类 `AuditudeSettings` 继承了此属性，但 `AdvertisingMetadata`不继承当前值。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. 要将广告准确地反映为滑动条上的提示，请聆听 `TimelineEvent`。 `TIMELINE_UPDATED` 并在您每次收到此活动时重绘划动栏。

   当VoD流使用延迟的广告加载时，并非当您的播放器进入PREPARED状态时，所有广告都会放在时间轴上，因此您必须显式重绘划动栏。

   TVSDK会优化此事件的调度，以最大限度地减少您必须重绘划动条的次数；因此，时间轴事件的数量与要放置在时间轴上的广告分段数无关。 例如，如果您有五个广告中断，则可能不会收到五个事件。

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

