---
description: 此示例显示了在播放时间线中包含TimeRange规范的推荐方式。
seo-description: 此示例显示了在播放时间线中包含TimeRange规范的推荐方式。
seo-title: 将时间范围广告标记放在时间轴上
title: 将时间范围广告标记放在时间轴上
uuid: 12935eba-2e91-40ea-a60e-02d0060c3cce
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 将时间范围广告标记放在时间轴上 {#place-timerange-ad-markers-on-the-timeline}

此示例显示了在播放时间线中包含TimeRange规范的推荐方式。

1. 将带外广告定位信息转换为规范列 `TimeRange` 表(即类的实例 `TimeRange` )。
1. 使用规范集 `TimeRange` 填充类的一个实 `TimeRangeCollection` 例。
1. 将可从实例获取的元数据实例 `TimeRangeCollection` 传递到方法( `replaceCurrentItem` MediaPlayer界面的一部分)。
1. 等待TVSDK通过等待 `PREPARED` 触发回调而转 `PlaybackEventListener#onPrepared` 换到状态。
1. 通过调用方法(界 `play()` 面的一部分)启动视 `MediaPlayer` 频播放。

* 处理时间轴冲突：有时某些规范在播放时 `TimeRange` 间轴上重叠。 例如，与规范对应的开始位置的 `TimeRange` 值可能低于已放置的结束位置的值。 在这种情况下，TVSDK将无提示地调整违规规范的开始位置，以 `TimeRange` 避免时间轴冲突。 通过此调整，新的 `TimeRange` 时间将比最初指定的时间短。 如果调整过于极端，以致导致持续时间为 `TimeRange` 零毫秒，TVSDK将静默地丢弃违规规 `TimeRange` 范。
* 当提 `TimeRange` 供自定义广告分段的规范时，TVSDK会尝试将它们转换为分组在广告分段内的广告。 TVSDK会查找相邻的规 `TimeRange` 范，并将它们分成不同的广告分段。 如果时间范围不与任何其他时间范围相邻，则这些时间范围会转换为包含单个广告的广告分段。
* 假定正在加载的媒体播放器项目指向VOD资产。 当应用程序尝试加载其元数据包含只能在自定义广告标记功能上下文中使用的规范的媒体资源时， `TimeRange` TVSDK会检查这一点。 如果基础资源不是VOD类型，则TVSDK库将引发异常。
* 处理自定义广告标记时，TVSDK会停用其他广告解析机制(通过Adobe Primetime广告决策（以前称为Auditude）或其他广告供应系统)。 您可以使用TVSDK提供的各种广告解析器模块或自定义广告标记机制之一。 使用自定义广告标记API时，广告内容被视为已解析并放置在时间轴上。

以下代码片断提供了一个简单的示例，其中将一组三个TimeRange规范作为自定义广告标记放在时间轴上。

```java>
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
TimeRangeCollection timeRanges = new TimeRangeCollection();  
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
 
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                               timeRanges.toMetadata(null)); 
 
// prepare the content for playback by creating 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentItem(mediaResource); 
// wait for TVSDK to reach the PREPARED state 
... 
MediaPlayer.PlaybackEventListener playbackEventListener = new 
  MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // TVSDK in in the PREPARED state. We are allowed to start the playback  
        mediaPlayer.play(); 
    } 
} 
```
