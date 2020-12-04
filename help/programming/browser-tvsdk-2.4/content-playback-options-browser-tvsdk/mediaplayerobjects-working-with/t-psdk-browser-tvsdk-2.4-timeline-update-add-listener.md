---
description: 要接收有关时间轴更新的通知，请注册相应的事件监听器。
seo-description: 要接收有关时间轴更新的通知，请注册相应的事件监听器。
seo-title: 为TimelineUpdatedEvent添加监听器
title: 为TimelineUpdatedEvent添加监听器
uuid: 7d742e15-5a55-4155-93a7-7b79f21c1472
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# 为TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}添加监听器

要接收有关时间轴更新的通知，请注册相应的事件监听器。

每次时间轴更新时，`MediaPlayer`都会调度类型为`AdobePSDK.PSDKEventType.TIMELINE_UPDATED`的`AdobePSDK.TimelineEvent`。
1. 实现适当的监听器。

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

