---
description: 您可以指定是否在加载所有广告并将其放置在时间轴中之前允许播放。 通过这种方式开始播放，查看器可以更快地访问主内容。 此功能仅适用于实时DVR，不能用于（例如VOD资产）。
title: 启用延迟广告加载
exl-id: 6b70a7ae-28ce-4a19-9560-26e937c721cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 启用延迟广告加载{#enable-lazy-ad-loading}

您可以指定是否在加载所有广告并将其放置在时间轴中之前允许播放。 通过这种方式开始播放，查看器可以更快地访问主内容。 此功能仅适用于实时DVR，不能用于（例如VOD资产）。

1. 使用布尔属性 `delayAdLoading` 在 `AdvertisingMetadata`.

   * 为false时，TVSDK会等待所有广告解析并置入后再转换为PREPARED状态。 默认情况下为false。
   * 为true时，TVSDK仅解析初始广告并转换为“已准备”状态。 剩余的广告将在播放期间解析并置入。

1. 要使用Adobe Primetime ad decisioning激活延迟的广告加载，请将此项设置为 `true` 当您创建 `AuditudeSettings`.

   此 `AuditudeSettings` 类从以下位置继承此属性 `AdvertisingMetadata`，但不继承当前值。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. 要在搓擦条上准确地将广告反映为提示，请聆听 `TimelineEvent`. `TIMELINE_UPDATED` 事件，并在每次收到此事件时重绘搓擦栏。

   当VoD流使用延迟的广告加载时，当播放器进入“已准备”状态时，并非所有广告都会放在时间轴上，因此您必须明确重绘推移栏。

   TVSDK将优化此事件的分发，以最大限度地减少必须重绘推移栏的次数；因此，时间线事件的数量与要在时间线上放置的广告插播数量无关。 例如，如果您有5个广告时间，则可能不会正好收到5个事件。

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```
