---
description: 此示例显示了在播放时间线中包含自定义广告标记的推荐方式。
seo-description: 此示例显示了在播放时间线中包含自定义广告标记的推荐方式。
seo-title: 在时间轴上放置自定义广告标记
title: 在时间轴上放置自定义广告标记
uuid: 47e31a97-e5da-46f3-bdcc-327c159c4355
translation-type: tm+mt
source-git-commit: 2a6ea34968ee7085931f99a24dfb23d097721b89
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# 在时间轴{#place-custom-ad-markers-on-the-timeline}上放置自定义广告标记

此示例显示了在播放时间线中包含自定义广告标记的推荐方式。

1. 将带外广告定位信息转换为`RepaceTimeRange`类的列表/数组。
1. 创建`CustomRangeMetadata`类的实例，并将其`setTimeRangeList`方法与列表/数组一起使用作为其参数来设置其时间范围列表。
1. 使用其`setType`方法将类型设置为`MARK_RANGE`。
1. 将`MediaPlayerItemConfig.setCustomRangeMetadata`方法与`CustomRangeMetadata`实例一起使用作其参数，以设置自定义范围元数据。
1. 将`MediaPlayer.replaceCurrentResource`方法与`MediaPlayerItemConfig`实例一起使用作其参数，以设置新资源为当前资源。
1. 等待`STATE_CHANGED`事件，它报告播放器处于`PREPARED`状态。
1. 通过调用`MediaPlayer.play`开始视频播放。

以下是完成此示例中的任务的结果：

* 如果`ReplaceTimeRange`在播放时间线上与另一个重叠，例如，`ReplaceTimeRange`的开始位置早于已放置的结束位置，则TVSDK将静默调整违规`ReplaceTimeRange`的开始以避免冲突。

   这使调整后的`ReplaceTimeRange`比最初指定的短。 如果调整导致持续时间为零，则TVSDK将静默删除违规的`ReplaceTimeRange`。

* TVSDK会查找相邻的自定义广告分段时间范围，并将它们分为单独的广告分段。

与任何其他时间范围不相邻的时间范围会转换为包含单个广告的广告分段。

* 如果应用程序尝试加载其配置包含`CustomRangeMetadata`的媒体资源，该配置只能用于上下文自定义广告标记，则如果基础资源不是VOD类型，TVSDK将引发异常。

* 在处理自定义广告标记时，TVSDK会停用其他广告解析机制(例如，Adobe Primetime广告决策)。

   您可以使用任何TVSDK广告解析器模块或自定义广告标记机制。 当您使用自定义广告标记时，广告内容会被视为已解析并放置在时间轴上。

下面的代码片断将三个时间范围作为自定义广告标记放置在时间轴上。

```java
// Assume that the 3 time ranges are obtained through external means 
// Use them to populate the ReplaceTimeRange instance 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 0)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.MARK_RANGE); 
 
//Create a MediaResource instance 
MediaResource mediaResource = MediaResource.createFromUrl( 
        "www.example.com/video/test_video.m3u8", timeRanges.toMedatada(null)); 
 
// Create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// Prepare the content for playback by calling replaceCurrentResource 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentResource(mediaResource, config); 
 
// wait for TVSDK to reach the PREPARED state 
mediaPlayer.addEventListener(MediaPlayerEvent.STATE_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
 
    if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
        // TVSDK is in the PREPARED state, so start the playback  
        mediaPlayer.play(); 
    } 
    ... 
}
```
