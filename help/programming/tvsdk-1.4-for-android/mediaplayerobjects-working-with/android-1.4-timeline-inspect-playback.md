---
description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义拖拽栏控件时，此控件最有用，在该控件中可识别与广告内容对应的内容部分。
seo-description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义拖拽栏控件时，此控件最有用，在该控件中可识别与广告内容对应的内容部分。
seo-title: Inspect播放时间轴
title: Inspect播放时间轴
uuid: b5ede131-1037-449b-bc3f-a066fdc92fc5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Inspect播放时间线{#inspect-the-playback-timeline}

您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义拖拽栏控件时，此控件最有用，在该控件中可识别与广告内容对应的内容部分。

下面是一个示例实现，如下面的屏幕截图所示。  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. 使用`getTimeline`方法访问`MediaPlayer`中的`Timeline`对象。

   `Timeline`类封装与与`MediaPlayer`实例当前加载的媒体项相关的时间线内容相关的信息。 `Timeline`类提供对基础时间轴的只读视图的访问。 `Timeline`类提供getter方法，该方法通过`TimelineMarker`对象的列表提供迭代器。

1. 对`TimelineMarkers`的列表进行迭代，并使用返回的信息来实现时间轴。

       “TimelineMarker”对象包含两条信息：
   
   * 标记在时间轴上的位置（以毫秒为单位）
   * 时间轴上标记的持续时间（以毫秒为单位）

1. 实现监听器回调接口`MediaPlayer.PlaybackEventListener.onTimelineUpdated`，并将其注册到`Timeline`对象。

   `Timeline`对象可以通过调用`OnTimelineUpdated`监听器通知您的应用程序在播放时间线中可能发生的更改。

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

