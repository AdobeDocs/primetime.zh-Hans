---
description: 此示例说明在播放时间轴上包含自定义广告标记的推荐方法。
title: 在时间轴上放置自定义广告标记
exl-id: 32a4b342-1f26-42c5-9682-789c541f0fa6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 在时间轴上放置自定义广告标记 {#place-custom-ad-markers-on-the-timeline}

此示例说明在播放时间轴上包含自定义广告标记的推荐方法。

1. 将带外广告定位信息转换为列表/阵列 `RepaceTimeRange` 类。
1. 创建实例 `CustomRangeMetadata` 类，并使用其 `setTimeRangeList` 方法使用list/array作为其参数，以设置其时间范围列表。
1. 使用其 `setType` 将类型设置为的方法 `MARK_RANGE`.
1. 使用 `MediaPlayerItemConfig.setCustomRangeMetadata` 方法 `CustomRangeMetadata` 实例作为参数，以设置自定义范围元数据。
1. 使用 `MediaPlayer.replaceCurrentResource` 方法 `MediaPlayerItemConfig` 将实例作为参数，以设置新资源。
1. 等待 `STATE_CHANGED` 事件，用于报告播放器位于 `PREPARED` 省/州。
1. 通过调用开始视频播放 `MediaPlayer.play`.

以下是完成此示例中任务的结果：

* 如果 `ReplaceTimeRange` 与播放时间轴上的另一个项目重叠，例如， `ReplaceTimeRange` 早于已放置的结束位置，TVSDK会静默地调整违规的开头 `ReplaceTimeRange` 以避免冲突。

   这使得调整后的 `ReplaceTimeRange` 比最初指定的短。 如果调整导致持续时间为零，则TVSDK静默地丢弃违规内容 `ReplaceTimeRange`.

* TVSDK会为自定义广告时间查找相邻的时间范围，并将其聚类为单独的广告时间。

与任何其他时间范围不相邻的时间范围将转换为包含单个广告的广告时间。

* 如果应用程序尝试加载的媒体资源配置包含 `CustomRangeMetadata` 如果基础资产不是VOD类型，则TVSDK会引发异常。

* 处理自定义广告标记时，TVSDK会停用其他广告解析机制(例如Adobe Primetime广告决策)。

   您可以使用任何TVSDK广告解析程序模块或自定义广告标记机制。 使用自定义广告标记时，广告内容会被视为已解析并放置在时间轴上。

以下代码片段将三个时间范围作为自定义广告标记放置在时间轴上。

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
