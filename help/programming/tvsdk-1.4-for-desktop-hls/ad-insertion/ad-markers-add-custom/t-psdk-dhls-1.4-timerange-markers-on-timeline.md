---
description: 此示例显示了在播放时间轴中包含TimeRange规范的建议方法。
title: 将时间范围广告标记置于时间轴上
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# 将TimeRange和标记放置到时间轴{#place-timerange-ad-markers-on-the-timeline}

此示例显示了在播放时间轴中包含TimeRange规范的建议方法。

1. 将带外广告定位信息转换为`TimeRange`规范（即`TimeRange`类的实例）的列表。
1. 使用`TimeRange`规范集填充`TimeRangeCollection`类的实例。
1. 将可从`TimeRangeCollection`实例获取的Metadata实例传递给`replaceCurrentItem`方法（`MediaPlayer`接口的一部分）。
1. 等待TVSDK过渡到PREPARED状态，方法是等待触发`PlaybackEventListener#onPrepared`回调。
1. 开始视频播放，方法是调用`play()`方法（`MediaPlayer`接口的一部分）。

* 处理时间轴冲突：有时某些`TimeRange`规范在播放时间线上重叠。 例如，与`TimeRange`规格对应的开始位置值可能低于已放置的结束位置值。 在这种情况下，TVSDK将静默调整违规`TimeRange`规范的开始位置以避免时间线冲突。 通过此调整，新`TimeRange`将变得比最初指定的更短。 如果调整过于极端，以致于会导致持续时间为零毫秒的`TimeRange`，则TVSDK将静默地删除违规的`TimeRange`规范。

* 当提供自定义广告分段的`TimeRange`规范时，TVSDK会尝试将这些规范转换为分组在广告分段内的广告。 TVSDK查找相邻的`TimeRange`规范，并将它们分成不同的广告分段。 如果有时间范围不与任何其他时间范围相邻，则这些时间范围会转换为包含单个广告的广告分段。

* 假定正在加载的媒体播放器项目指向VOD资产。 当您的应用程序尝试加载其元数据包含`TimeRange`规范的媒体资源时，TVSDK会检查这一点，这些规范只能在自定义广告标记功能的上下文中使用。 如果基础资源不是VOD类型，TVSDK库将引发异常。

* 在处理自定义广告标记时，TVSDK会停用其他广告解析机制(通过Adobe Primetime广告决策（以前称为Auditude）或其他广告供应系统)。 您可以使用TVSDK提供的各种广告解析器模块或自定义广告标记机制之一。 使用自定义广告标记API时，广告内容被视为已解析并放置在时间轴上。

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

以下代码片断提供了一个简单示例，其中一组由三个`TimeRange`规范组成的规范作为自定义广告标记放置在时间轴上。

```
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
var timeRanges:TimeRangeCollection = new TimeRangeCollection(); 
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
  
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                             timeRanges.toMetadata(null));
```
