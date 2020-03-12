---
description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义划动栏控件时，这最有用。在该控件中，标识了与广告内容相对应的内容部分。
seo-description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义划动栏控件时，这最有用。在该控件中，标识了与广告内容相对应的内容部分。
seo-title: 检查播放时间轴
title: 检查播放时间轴
uuid: b5ede131-1037-449b-bc3f-a066fdc92fc5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 检查播放时间轴{#inspect-the-playback-timeline}

您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义划动栏控件时，这最有用。在该控件中，标识了与广告内容相对应的内容部分。

下面是一个示例实现，如以下屏幕截图所示。  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. 使用 `Timeline` 方法访问 `MediaPlayer` 中的对 `getTimeline` 象。

   类封 `Timeline` 装与时间轴内容相关的信息，该时间轴内容与实例当前加载的媒体项相关联 `MediaPlayer` 。 该 `Timeline` 类允许访问基础时间轴的只读视图。 类提 `Timeline` 供了getter方法，该方法通过对象列表提供迭代 `TimelineMarker` 器。

1. 遍历列表并使用 `TimelineMarkers` 返回的信息来实现时间轴。

       “TimelineMarker”对象包含两条信息：
   
   * 标记在时间轴上的位置（以毫秒为单位）
   * 时间轴上标记的持续时间（以毫秒为单位）

1. 实现监听器回调接 `MediaPlayer.PlaybackEventListener.onTimelineUpdated` 口并向对象注册该 `Timeline` 接口。

   该对 `Timeline` 象可以通过调用监听器来通知应用程序在播放时间线中可能发生的 `OnTimelineUpdated` 更改。

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
// iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
while (iterator.hasNext()) { 
   TimelineMarker marker = iterator.next(); 
   // the start position of the marker 
   long startPos = marker.getTime(); 
   // the duration of the marker 
   long duration = marker.getDuration(); 
}
```

