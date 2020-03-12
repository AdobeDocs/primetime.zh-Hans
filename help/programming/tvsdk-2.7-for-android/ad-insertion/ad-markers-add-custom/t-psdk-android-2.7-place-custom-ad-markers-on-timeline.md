---
description: 此示例显示了在播放时间线上包含自定义广告标记的推荐方法。
seo-description: 此示例显示了在播放时间线上包含自定义广告标记的推荐方法。
seo-title: 在时间轴上放置自定义广告标记
title: 在时间轴上放置自定义广告标记
uuid: ee74d1f3-7186-44b8-bad7-55af579842e8
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 在时间轴上放置自定义广告标记 {#place-custom-ad-markers-on-the-timeline}

此示例显示了在播放时间线上包含自定义广告标记的推荐方法。

1. 将带外广告定位信息转换为类的列表／数 `RepaceTimeRange` 组。
1. 创建类的实 `CustomRangeMetadata` 例，并使用其方法 `setTimeRangeList` ，将list/array作为其参数来设置其时间范围列表。
1. 使用其 `setType` 方法将类型设置为 `MARK_RANGE`。
1. 将该方 `MediaPlayerItemConfig.setCustomRangeMetadata` 法与实例 `CustomRangeMetadata` 一起使用，以设置自定义范围元数据。
1. 使用 `MediaPlayer.replaceCurrentResource` 将实例作为 `MediaPlayerItemConfig` 参数的方法设置新资源为当前资源。
1. 等待一 `STATE_CHANGED` 个事件，该事件报告播放器处于状 `PREPARED` 态。
1. 通过调用启动视频播放 `MediaPlayer.play`。

以下是完成此示例中任务的结果：>
* 例如， `ReplaceTimeRange` 如果播放时间线上的另一个重叠，则一个的开始位置早于已放置的结束位置，TVSDK将静默地调整违规的开始 `ReplaceTimeRange``ReplaceTimeRange` 以避免冲突。

   这会使调整后的内 `ReplaceTimeRange` 容比最初指定的更短。 如果调整导致持续时间为零，TVSDK将静默删除违规 `ReplaceTimeRange`。

* TVSDK会查找相邻的自定义广告分段时间范围，并将它们分为多个单独的广告分段。

   与任何其他时间范围不相邻的时间范围会转换为包含单个广告的广告分段。
* 如果应用程序尝试加载其配置包含的媒体资源（该配置仅可用于上下文自定义广告标记），则如果基础资源不是VOD类型， `CustomRangeMetadata` TVSDK将引发异常。
* 处理自定义广告标记时，TVSDK会停用其他广告解析机制（例如，Adobe Primetime广告决策）。

   您可以使用任何TVSDK广告解析器模块或自定义广告标记机制。 当您使用自定义广告标记时，广告内容会被视为已解析并放置在时间轴上。

以下代码片断将三个时间范围作为自定义广告标记放置在时间轴上。

>```java>
>// Assume that the 3 time ranges are obtained through external means 
>// Use them to populate the ReplaceTimeRange instance 
>List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
>timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
>timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
>timeRanges.add(new ReplaceTimeRange(25000,30000, 0)); 
> 
>
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
>customRangeMetadata.setTimeRangeList(timeRanges); 
>customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.MARK_RANGE); 
> 
>
//Create a MediaResource instance 
>MediaResource mediaResource = MediaResource.createFromUrl( 
>               "www.example.com/video/test_video.m3u8", timeRanges.toMedatada(null)); 
> 
>
// Create a MediaPlayerItemConfig instance 
>MediaPlayerItemConfig config =  
>   new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
> 
>
// Set customRangeMetadata 
>config.setCustomRangeMetadata(customRangeMetadata); 
> 
>
// Prepare the content for playback by calling replaceCurrentResource 
>// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
>mediaPlayer.replaceCurrentResource(mediaResource, config); 
> 
>
// wait for TVSDK to reach the PREPARED state 
>mediaPlayer.addEventListener(MediaPlayerEvent.STATE_CHANGED,  
>   new StatusChangeEventListener() { 
>       @Override 
>       public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
> 
>    
   if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
>               // TVSDK is in the PREPARED state, so start the playback  
>               mediaPlayer.play(); 
>       } 
>       ... 
>}
>```
