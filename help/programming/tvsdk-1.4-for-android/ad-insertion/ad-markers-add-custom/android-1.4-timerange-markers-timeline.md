---
description: 此示例显示了在播放时间轴上包含TimeRange规范的推荐方式。
seo-description: 此示例显示了在播放时间轴上包含TimeRange规范的推荐方式。
seo-title: 将时间范围广告标记放置在时间轴上
title: 将时间范围广告标记放置在时间轴上
uuid: 12935eba-2e91-40ea-a60e-02d0060c3cce
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# 将TimeRange广告标记放置在时间轴{#place-timerange-ad-markers-on-the-timeline}上

此示例显示了在播放时间轴上包含TimeRange规范的推荐方式。

1. 将带外广告定位信息转换为`TimeRange`规范的列表（即`TimeRange`类的实例）。
1. 使用`TimeRange`规范集填充`TimeRangeCollection`类的实例。
1. 将可从`TimeRangeCollection`实例获取的元数据实例传递给`replaceCurrentItem`方法（MediaPlayer接口的一部分）。
1. 等待TVSDK过渡到`PREPARED`状态，等待触发`PlaybackEventListener#onPrepared`回调。
1. 通过调用`play()`方法（`MediaPlayer`接口的一部分）开始视频播放。

* 处理时间轴冲突：有时，播放时间轴上的某些`TimeRange`规范会重叠。 例如，与`TimeRange`规格对应的开始位置的值可能低于已放置的结束位置的值。 在这种情况下，TVSDK将静默调整违规`TimeRange`规范的开始位置，以避免时间线冲突。 通过此调整，新`TimeRange`变得比最初指定的更短。 如果调整过程极端，以致于会导致持续时间为0 ms的`TimeRange`,TVSDK将静默地删除违规的`TimeRange`规范。
* 当提供自定义广告分段的`TimeRange`规范时，TVSDK会尝试将这些规范转换为广告分段内分组的广告。 TVSDK查找相邻的`TimeRange`规范，并将它们分成单独的广告分段。 如果有时间范围不与任何其他时间范围相邻，则它们会转换为包含单个广告的广告分段。
* 假定正在加载的媒体播放器项目指向VOD资产。 当应用程序尝试加载其元数据包含`TimeRange`规范的媒体资源时，TVSDK会检查这一点，这些规范只能在自定义广告标记功能的上下文中使用。 如果基础资源不是VOD类型，TVSDK库将引发异常。
* 在处理自定义广告标记时，TVSDK会停用其他广告解析机制(通过Adobe Primetime广告决策（以前称为Auditude）或其他广告供应系统)。 您可以使用TVSDK提供的各种广告解析程序模块或自定义广告标记机制。 使用自定义广告标记API时，广告内容被视为已解析并放置在时间轴上。

下面的代码片断提供了一个简单的示例，其中将一组三个TimeRange规范作为自定义广告标记放置在时间轴上。

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
