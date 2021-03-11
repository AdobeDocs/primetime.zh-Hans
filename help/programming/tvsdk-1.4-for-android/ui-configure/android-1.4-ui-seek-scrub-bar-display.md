---
description: TVSDK支持搜索到某个特定位置（时间），在该位置，流是视频点播(VOD)和直播流中的滑动窗口播放列表。
title: 使用当前播放位置显示搜索拖拉栏
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# 显示当前播放位置{#display-a-seek-scrub-bar-with-the-current-playback-position}的搜索滑动条

TVSDK支持搜索到某个特定位置（时间），在该位置，流是视频点播(VOD)和直播流中的滑动窗口播放列表。

>[!IMPORTANT]
>
>仅DVR允许在实时流中搜索。

1. 设置搜索回呼。

       搜索是异步的，因此TVSDK调度以下与搜索相关的事件:
   
   * `QOSEventListener.onSeekStart`  — 开始搜寻。
   * `QOSEventListener.onSeekComplete`  — 寻求成功。
   * `QOSEventListener.onOperationFailed`  — 搜索失败。

1. 等待播放器处于有效状态进行搜索。

   有效状态包括PREPARED、COMPLETE、PAUSED和PLAYING。

1. 使用本机SeekBar设置`OnSeekBarChangeListener`以查看用户正在擦洗的时间。
1. 侦听`QOSEventListener.onOperationFailed`并采取相应的操作。

   此事件传递相应的警告。 例如，应用程序决定如何继续，方法是再次尝试搜索或从上一个位置继续播放。

1. 等待TVSDK调用`QOSEventListener.onSeekComplete`回调。
1. 使用回调的位置参数检索最终调整的播放位置。

   这很重要，因为搜索后的实际开始位置可能与请求的位置不同。 如果搜索或其他重新定位在广告中断的中间结束或跳过广告中断，则播放行为可能会受到影响。

1. 显示搜索拖拽栏时使用位置信息。

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**搜索示例**

在本例中，用户将搜索条滑动到所需位置。

```java
// Use the native SeekBar to set OnSeekBarChangeListener to  
//see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) {  
            // Update the seek bar thumb, with the position provided by the user. 
            setPosition(progress); 
        } 
    } 
 
    @Override 
    public void onStartTrackingTouch(SeekBar seekBar) { 
        isSeeking = true; 
    } 
 
    @Override 
    public void onStopTrackingTouch(SeekBar seekBar) { 
        isSeeking = false; 
        // Retrieve the playback range. 
        TimeRange playbackRange = mediaPlayer.getPlaybackRange(); 
        // Make sure to seek inside the playback range. 
        long seekPosition = Math.min(Math.round(seekBar.getProgress()),  
                                     playbackRange.getDuration()); 
        // Perform seek. 
        seek(playbackRange.getBegin() + seekPosition); 
    } 
}; 
```

