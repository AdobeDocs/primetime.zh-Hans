---
description: TVSDK支持搜索到某个特定位置（时间），在该位置，流是视频点播(VOD)和实时流中的滑动窗口播放列表。
seo-description: TVSDK支持搜索到某个特定位置（时间），在该位置，流是视频点播(VOD)和实时流中的滑动窗口播放列表。
seo-title: 显示具有当前播放位置的搜索滑动条
title: 显示具有当前播放位置的搜索滑动条
uuid: a9f4dd6c-78cf-455c-8c31-b2f7b740d84a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 显示具有当前播放位置的搜索滑动条 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支持搜索到某个特定位置（时间），在该位置，流是视频点播(VOD)和实时流中的滑动窗口播放列表。

>[!IMPORTANT]
>
>仅DVR允许在实时流中搜索。

1. 设置搜索回调。

       搜索是异步的，因此TVSDK会调度以下与搜索相关的事件：
   
   * `QOSEventListener.onSeekStart` -开始搜索。
   * `QOSEventListener.onSeekComplete` -寻求成功。
   * `QOSEventListener.onOperationFailed` -搜索失败。

1. 等待播放器处于有效状态进行搜索。

   有效状态包括PREPARED、COMPLETE、PAUSED和PLAYING。

1. 使用本机SeekBar设置 `OnSeekBarChangeListener` 为查看用户拖拽的时间。
1. 倾听并 `QOSEventListener.onOperationFailed` 采取适当的行动。

   此事件会传递相应的警告。 例如，您的应用程序确定如何继续，方法是再次尝试搜索或从上一个位置继续回放。

1. 等待TVSDK调用回 `QOSEventListener.onSeekComplete` 调。
1. 使用回调的位置参数检索最终调整的播放位置。

   这很重要，因为搜索后的实际开始位置可能与请求的位置不同。 如果搜索或其他重新定位在广告中断的中间结束或跳过广告中断，则播放行为可能会受到影响。

1. 显示搜索拖拽栏时，请使用位置信息。

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**搜索示例**

在此示例中，用户将搜索栏拖动到所需位置。

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

