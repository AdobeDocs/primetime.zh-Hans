---
description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间线描述。 当应用程序显示自定义推式栏控件，并在该控件中标识与广告内容对应的内容部分时，此功能非常有用。
title: Inspect播放时间轴
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Inspect播放时间轴{#inspect-the-playback-timeline}

您可以获取与TVSDK正在播放的当前选定项目关联的时间线描述。 当应用程序显示自定义推式栏控件，并在该控件中标识与广告内容对应的内容部分时，此功能非常有用。

以下是如下面的屏幕截图中所看到的实施示例。
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. 访问 `Timeline` 中的对象 `MediaPlayer` 使用 `get` 方法。

   此 `Timeline` 类封装与时间轴内容相关的信息，该时间轴与当前由加载的媒体项目相关联 `MediaPlayer` 实例。 此 `Timeline` 类提供对基础时间线的只读视图的访问权限。 此 `Timeline` 类提供了用于获取所有放置的getter方法 `TimelineMarker` 对象。

1. 循环访问列表 `TimelineMarkers` 并使用返回的信息实施您的时间线。

       “TimelineMarker”对象包含两条信息：
   
   * 标记在时间轴上的位置（以毫秒为单位）
   * 标记在时间轴上的持续时间（以毫秒为单位）

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
