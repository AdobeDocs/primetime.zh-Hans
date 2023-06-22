---
description: 要接收有关时间线更新的通知，请注册适当的事件侦听器。
title: 为TimelineUpdatedEvent添加侦听器
exl-id: 7b55beb5-fd84-4144-8d02-bbd998f99e3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# 为TimelineUpdatedEvent添加侦听器{#add-listeners-for-timelineupdatedevent}

要接收有关时间线更新的通知，请注册适当的事件侦听器。

每次更新时间线时， `MediaPlayer` 调度 `AdobePSDK.TimelineEvent` 带有类型 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
1. 实施相应的侦听器。

   ```js
   function onTimelineUpdatedEvent(event) { 
       var timelineMarkers = event.timeline.timelineMarkers; 
       //add code to remove old timeline markers from scrub-bar. 
       var range = player.playbackRange; 
       //iterate through the list of timelineMarkers 
       for(var i = 0; i < timelineMarkers.length; i++) 
       { 
           var markerLocalTime = timelineMarkers[i].localRange.begin; 
           var markerVirtualTime = timelineMarkers[i].virtualRange.begin; 
           var duration = timelineMarkers[i].duration; 
        // add code to draw a particular marker on scrub-bar 
       }      
   }
   ```

1. 注册事件侦听器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```
