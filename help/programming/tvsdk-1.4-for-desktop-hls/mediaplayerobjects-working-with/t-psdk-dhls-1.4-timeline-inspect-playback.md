---
description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义拖拽栏控件时，此控件最有用，在该控件中可识别与广告内容对应的内容部分。
seo-description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义拖拽栏控件时，此控件最有用，在该控件中可识别与广告内容对应的内容部分。
seo-title: Inspect播放时间轴
title: Inspect播放时间轴
uuid: 2f903493-2d88-4af2-ac71-36300b49735b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Inspect播放时间线{#inspect-the-playback-timeline}

您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义拖拽栏控件时，此控件最有用，在该控件中可识别与广告内容对应的内容部分。

下面是一个示例实现，如下面的屏幕截图所示。
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. 使用`get`方法访问`MediaPlayer`中的`Timeline`对象。

   `Timeline`类封装与与`MediaPlayer`实例当前加载的媒体项相关的时间线内容相关的信息。 `Timeline`类提供对基础时间轴的只读视图的访问。 `Timeline`类提供getter方法，用于获取所有已放置的`TimelineMarker`对象。

1. 对`TimelineMarkers`的列表进行迭代，并使用返回的信息来实现时间轴。

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

