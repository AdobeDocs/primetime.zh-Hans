---
description: 您可以指定是否在所有广告加载并放置在时间轴中之前允许播放。 以这种方式开始播放可使查看者更快地访问主内容。 此功能仅适用于实时DVR，不适用于VOD资源等。
title: 启用延迟广告加载
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# 启用延迟广告加载{#enable-lazy-ad-loading}

您可以指定是否在所有广告加载并放置在时间轴中之前允许播放。 以这种方式开始播放可使查看者更快地访问主内容。 此功能仅适用于实时DVR，不适用于VOD资源等。

1. 使用`AdvertisingMetadata`中的布尔属性`delayAdLoading`。

   * 如果为false，则TVSDK会等到所有广告都解析并放置后，才转换为PREPARED状态。 默认情况下为false。
   * 如果为true，则TVSDK仅将初始广告和过渡解析为PREPARED状态。 其余广告在播放过程中进行解析和放置。

1. 要还通过Adobe Primetime广告决策激活延迟广告加载，请在创建`AuditudeSettings`时将其设置为`true`。

   `AuditudeSettings`类从`AdvertisingMetadata`继承此属性，但不继承当前值。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. 要将广告准确反映为滑动条上的提示，请聆听`TimelineEvent`。 `TIMELINE_UPDATED` 每次收到此事件时，事件并重新绘制划动栏。

   当VoD流使用延迟广告加载时，并非当您的播放器进入PREPARED状态时所有广告都放在时间轴上，因此您必须显式重绘划动栏。

   TVSDK将优化此事件的派单，以最大限度地减少您重绘拖拉条的次数；因此，时间轴事件的数量与要置于时间轴上的广告分页数无关。 例如，如果您有五个广告中断，则可能不会收到五个事件。

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

