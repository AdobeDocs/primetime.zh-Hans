---
description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间轴描述。 当您的应用程序显示自定义推移栏控件时，这非常有用，在该控件中可识别与广告内容对应的内容部分。
title: Inspect播放时间轴
exl-id: 38b5ce0e-5554-462e-986f-f3864f7cf879
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Inspect播放时间轴{#inspect-the-playback-timeline}

您可以获取与TVSDK正在播放的当前选定项目关联的时间轴描述。 当您的应用程序显示自定义推移栏控件时，这非常有用，在该控件中可识别与广告内容对应的内容部分。

以下是一个实施示例，如以下屏幕快照中所示。
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. 访问 `Timeline` 对象 `MediaPlayer` 使用 `get` 方法。

   的 `Timeline` 类封装与时间轴内容相关的信息，该时间轴内容与当前由加载的媒体项目相关联 `MediaPlayer` 实例。 的 `Timeline` 类提供对基础时间轴的只读视图的访问权限。 的 `Timeline` 类提供用于获取所有已放置的getter方法 `TimelineMarker` 对象。

1. 遍历 `TimelineMarkers` 并使用返回的信息来实施时间轴。

       “时间轴标记”对象包含两条信息：
   
   * 标记在时间轴上的位置（以毫秒为单位）
   * 时间轴上标记的持续时间（以毫秒为单位）

<!--<a id="example_BA936629E82B4082A2E2C548E3FC3357"></a>-->

```
// access the timeline object 
var timeline:Timeline = mediaPlayer.timeline; 
 
// iterate through the list of TimelineMarkers 
var markers:Vector.<TimelineMarker> = timeline.timelineMarkers; 
markers.forEach(function(item:TimelineMarker,  
                         index:int,  
                         vector:Vector.<TimelineMarker>):void { 
    
    // the start position of the marker 
    var startPos:Number = item.time; 
 
    // the duration of the marker 
    var duration:Number = item.duration; 
 
    // draw the marker on the scrub-bar 
}
```
