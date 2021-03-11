---
description: 要接收有关时间轴更新的通知，请注册相应的事件侦听器。
title: 为TimelineUpdatedEvent添加侦听器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# 为TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}添加侦听器

要接收有关时间轴更新的通知，请注册相应的事件侦听器。

每次时间轴更新时，`MediaPlayer`都会调度类型为`AdobePSDK.PSDKEventType.TIMELINE_UPDATED`的`AdobePSDK.TimelineEvent`。
1. 实施适当的监听器。

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

1. 注册事件监听器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```

