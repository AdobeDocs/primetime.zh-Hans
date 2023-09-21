---
description: 要接收有关时间线更新的通知，请注册相应的事件侦听器。
title: 为TimelineUpdatedEvent添加侦听器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# 为TimelineUpdatedEvent添加侦听器{#add-listeners-for-timelineupdatedevent}

要接收有关时间线更新的通知，请注册相应的事件侦听器。

每次更新时间线时， `MediaPlayer` 调度 `AdobePSDK.TimelineEvent` 带有类型 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
1. 实施相应的监听程序。

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
