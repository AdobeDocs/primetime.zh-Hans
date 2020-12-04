---
description: TVSDK支持在视频点播(VOD)和直播流中搜索流是滑动窗口播放列表的特定位置（时间）。
seo-description: TVSDK支持在视频点播(VOD)和直播流中搜索流是滑动窗口播放列表的特定位置（时间）。
seo-title: 显示具有当前播放位置的搜索滑动条
title: 显示具有当前播放位置的搜索滑动条
uuid: a9f4dd6c-78cf-455c-8c31-b2f7b740d84a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# 显示当前播放位置{#display-a-seek-scrub-bar-with-the-current-playback-position}的搜索滑动条

TVSDK支持在视频点播(VOD)和直播流中搜索流是滑动窗口播放列表的特定位置（时间）。

>[!IMPORTANT]
>
>在实时流中搜索仅允许DVR。

1. 设置搜索回呼。

       搜索是异步的，因此TVSDK将分派以下搜索相关事件:
   
   * `QOSEventListener.onSeekStart` -开始寻找。
   * `QOSEventListener.onSeekComplete` -寻求成功。
   * `QOSEventListener.onOperationFailed` -搜索失败。

1. 等待播放器处于有效状态进行搜索。

   有效状态包括PREPARED、COMPLETE、PAUSED和PLAYING。

1. 使用本机SeekBar设置`OnSeekBarChangeListener`以查看用户正在擦洗的时间。
1. 侦听`QOSEventListener.onOperationFailed`并采取适当的操作。

   此事件会传递相应的警告。 例如，您的应用程序决定如何继续，方法是再次尝试搜索或从上一个位置继续播放。

1. 等待TVSDK调用`QOSEventListener.onSeekComplete`回调。
1. 使用回调的位置参数检索最终调整的播放位置。

   这很重要，因为搜索后的实际开始位置可能与请求的位置不同。 如果搜索或其他重新定位在广告中间结束或跳过广告中间，则播放行为可能会受到影响。

1. 在显示搜索拖拽栏时使用位置信息。

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**搜索示例**

在此示例中，用户将搜索条擦到所需位置。

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

