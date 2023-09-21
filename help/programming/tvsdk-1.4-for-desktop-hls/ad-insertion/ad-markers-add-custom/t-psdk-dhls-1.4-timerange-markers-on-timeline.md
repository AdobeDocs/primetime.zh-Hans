---
description: 此示例说明在播放时间轴上包含TimeRange规范的建议方法。
title: 在时间轴上放置TimeRange广告标记
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 在时间轴上放置TimeRange广告标记 {#place-timerange-ad-markers-on-the-timeline}

此示例说明在播放时间轴上包含TimeRange规范的建议方法。

1. 将带外广告定位信息转换为列表 `TimeRange` 规范(即 `TimeRange` 类)。
1. 使用集合 `TimeRange` 用于填充实例的 `TimeRangeCollection` 类。
1. 传递元数据实例，该实例可从 `TimeRangeCollection` 实例，到 `replaceCurrentItem` 方法（的一部分） `MediaPlayer` 界面)。
1. 等待TVSDK转换为“已准备”状态，方法是 `PlaybackEventListener#onPrepared` 要触发的回调。
1. 通过调用 `play()` 方法（的一部分） `MediaPlayer` 界面)。

* 处理时间线冲突：在某些情况下， `TimeRange` 规范在播放时间轴上重叠。 例如，对应于起始位置的值 `TimeRange` 规范可能低于已放置的结束位置的值。 在这种情况下，TVSDK会静默地调整违规的开始位置 `TimeRange` 规范以避免时间线冲突。 通过这种调整，新的 `TimeRange` 将变得比最初指定的更短。 如果这种调整是如此极端，以致于会导致 `TimeRange` 在持续时间为零毫秒的情况下，TVSDK可静默丢弃违规内容 `TimeRange` 规范。

* 时间 `TimeRange` 其中提供了自定义广告时间的规范，TVSDK会尝试将这些时间转换为在广告时间中分组的广告。 TVSDK查找相邻的 `TimeRange` 规范并将它们聚类为单独的广告时间。 如果存在不与任何其他时间范围相邻的时间范围，则会将它们转换为包含单个广告的广告时间。

* 假定正在加载的媒体播放器项目指向VOD资源。 每当应用程序尝试加载其元数据包含的媒体资源时，TVSDK都会对此进行检查 `TimeRange` 只能在自定义广告标记功能上下文中使用的规范。 如果基础资产不是VOD类型，则TVSDK库会引发异常。

* 处理自定义广告标记时，TVSDK会停用其他广告解析机制(通过Adobe Primetime ad decisioning(以前称为Auditude)或其他广告配置系统)。 您可以使用TVSDK提供的各种广告解析程序模块之一或自定义广告标记机制。 使用自定义广告标记API时，广告内容被视为已解析并放置在时间轴上。

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

以下代码片段提供了一个简单的示例，其中一组包含 `TimeRange` 规范作为自定义广告标记放置在时间轴上。

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
