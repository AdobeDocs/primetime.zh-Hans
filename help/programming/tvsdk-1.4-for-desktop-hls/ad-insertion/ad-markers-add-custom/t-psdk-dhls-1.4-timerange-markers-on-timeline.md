---
description: 此示例显示了在播放时间轴上包含TimeRange规范的推荐方式。
seo-description: 此示例显示了在播放时间轴上包含TimeRange规范的推荐方式。
seo-title: 将时间范围广告标记放置在时间轴上
title: 将时间范围广告标记放置在时间轴上
uuid: cbcc4c84-0d56-4331-b555-b8e59f7d52d4
translation-type: tm+mt
source-git-commit: fd21a29bb186238142d43e0277bbf92f8406f6f7
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# 将时间范围广告标记放置在时间轴上 {#place-timerange-ad-markers-on-the-timeline}

此示例显示了在播放时间轴上包含TimeRange规范的推荐方式。

1. 将带外广告定位信息转换为规 `TimeRange` 范列表(即类的实 `TimeRange` 例)。
1. 使用规范集 `TimeRange` 填充类的实例 `TimeRangeCollection` 。
1. 将可从实例获取的元数据实 `TimeRangeCollection` 例传递给方 `replaceCurrentItem` 法(接口的一 `MediaPlayer` 部分)。
1. 等待TVSDK过渡到PREPARED状态，等待回 `PlaybackEventListener#onPrepared` 调被触发。
1. 开始视频播放 `play()` 方法(界面的 `MediaPlayer` 一部分)。

* 处理时间轴冲突：有时某些规范在播 `TimeRange` 放时间线上重叠。 例如，与规范对应的开始位 `TimeRange` 置的值可能低于已放置的结束位置的值。 在这种情况下，TVSDK将静默调整违规规范的开始位置， `TimeRange` 以避免时间线冲突。 通过此调整，新的 `TimeRange` 时间将比最初指定的时间短。 如果调整过度，导致持续时间为 `TimeRange` 零毫秒，TVSDK将静默删除违规规 `TimeRange` 范。

* 当提 `TimeRange` 供自定义广告分段的规范时，TVSDK会尝试将它们转换为在广告分段内分组的广告。 TVSDK会查找相邻的 `TimeRange` 规范并将它们分成不同的广告分段。 如果有时间范围不与任何其他时间范围相邻，则它们会转换为包含单个广告的广告分段。

* 假定正在加载的媒体播放器项目指向VOD资产。 当应用程序尝试加载其元数据包含规范的媒体资源时，TVSDK会 `TimeRange` 检查这一点，这些规范只能在自定义广告标记功能的上下文中使用。 如果基础资源不是VOD类型，TVSDK库将引发异常。

* 在处理自定义广告标记时，TVSDK会停用其他广告解析机制(通过Adobe Primetime广告决策（以前称为Auditude）或其他广告供应系统)。 您可以使用TVSDK提供的各种广告解析程序模块或自定义广告标记机制。 使用自定义广告标记API时，广告内容被视为已解析并放置在时间轴上。

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

下面的代码片断提供了一个简单的示例，其中，将一组 `TimeRange` 三个规范作为自定义广告标记放置在时间轴上。

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
