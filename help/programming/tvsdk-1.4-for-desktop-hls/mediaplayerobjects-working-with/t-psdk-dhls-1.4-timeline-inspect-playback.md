---
description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义划动栏控件时，这最有用。在该控件中，标识了与广告内容相对应的内容部分。
seo-description: 您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义划动栏控件时，这最有用。在该控件中，标识了与广告内容相对应的内容部分。
seo-title: 检查播放时间轴
title: 检查播放时间轴
uuid: 2f903493-2d88-4af2-ac71-36300b49735b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 检查播放时间轴{#inspect-the-playback-timeline}

您可以获取与TVSDK正在播放的当前选定项目关联的时间轴的描述。 当应用程序显示自定义划动栏控件时，这最有用。在该控件中，标识了与广告内容相对应的内容部分。

下面是一个示例实现，如以下屏幕截图所示。
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. 使用 `Timeline` 方法访问 `MediaPlayer` 中的对 `get` 象。

   类封 `Timeline` 装与时间轴内容相关的信息，该时间轴内容与实例当前加载的媒体项相关联 `MediaPlayer` 。 该 `Timeline` 类允许访问基础时间轴的只读视图。 类提 `Timeline` 供了获取所有已放置对象的getter方 `TimelineMarker` 法。

1. 遍历列表并使用 `TimelineMarkers` 返回的信息来实现时间轴。

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

