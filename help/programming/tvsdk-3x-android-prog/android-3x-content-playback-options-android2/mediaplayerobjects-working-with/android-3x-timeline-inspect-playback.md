---
description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间轴描述。 当您的应用程序显示自定义推移栏控件时，这非常有用，在该控件中可识别与广告内容对应的内容部分。
title: Inspect播放时间轴
exl-id: 95792354-76f6-44fd-9207-73e862b434e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect播放时间轴 {#inspect-the-playback-timeline}

您可以获取与TVSDK正在播放的当前选定项目关联的时间轴描述。 当您的应用程序显示自定义推移栏控件时，这非常有用，在该控件中可识别与广告内容对应的内容部分。

以下是一个实施示例，如以下屏幕快照中所示。  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. 访问 `Timeline` 对象 `MediaPlayer` 使用 `getTimeline()` 方法。

   的 `Timeline` 类封装与时间轴内容相关的信息，该时间轴内容与当前由加载的媒体项目相关联 `MediaPlayer` 实例。 的 `Timeline` 类提供对基础时间轴的只读视图的访问权限。 的 `Timeline` 类提供getter方法，该方法通过 `TimelineMarker` 对象。

1. 遍历 `TimelineMarkers` 并使用返回的信息来实施时间轴。

       “时间轴标记”对象包含两条信息：
   
   * 标记在时间轴上的位置（以毫秒为单位）
   * 时间轴上标记的持续时间（以毫秒为单位）

1. 听 `MediaPlayerEvent.TIMELINE_UPDATED` 事件 `MediaPlayer` 实例，并实施 `TimelineUpdatedEventListener.onTimelineUpdated()` 回调。

   的 `Timeline` 对象可以通过调用 `OnTimelineUpdated` 侦听器。

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
 
// Iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
 
while (iterator.hasNext()) { 
    TimelineMarker marker = iterator.next(); 
    // the start position of the marker 
    long startPos = marker.getTime(); 
    // the duration of the marker 
    long duration = marker.getDuration(); 
}
```
