---
description: 您可以获取与TVSDK正在播放的当前选定项目相关联的时间轴的描述。 当应用程序显示自定义划动栏控件时，此选项最有用。
title: Inspect播放时间轴
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Inspect播放时间轴{#inspect-the-playback-timeline}

您可以获取与TVSDK正在播放的当前选定项目相关联的时间轴的描述。 当应用程序显示自定义划动栏控件时，此选项最有用。

下面是一个示例实现，如下面的屏幕截图所示。
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. 使用`get`方法访问`MediaPlayer`中的`Timeline`对象。

   `Timeline`类封装与时间轴内容相关的信息，该时间轴内容与当前由`MediaPlayer`实例加载的媒体项关联。 `Timeline`类提供对基础时间轴的只读视图的访问。 `Timeline`类提供用于获取所有已放置`TimelineMarker`对象的getter方法。

1. 遍历`TimelineMarkers`的列表，并使用返回的信息来实现时间轴。

       “TimelineMarker”对象包含两条信息：
   
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

