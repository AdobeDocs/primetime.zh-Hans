---
description: TVSDK支持在视频点播(VOD)和实时流中搜索流是滑动窗口播放列表的特定位置（时间）。
title: 显示具有当前播放位置的搜寻拖拽栏
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 显示具有当前播放位置的搜寻拖拽栏 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支持在视频点播(VOD)和实时流中搜索流是滑动窗口播放列表的特定位置（时间）。

>[!IMPORTANT]
>
>仅允许在DVR中进行实时流搜寻。

1. 设置用于搜寻的回调。

       搜寻是异步执行的，因此TVSDK会调度以下与搜寻相关的事件：
   
   * `QOSEventListener.onSeekStart`  — 搜寻开始。
   * `QOSEventListener.onSeekComplete`  — 搜寻成功。
   * `QOSEventListener.onOperationFailed`  — 搜寻失败。

1. 等待播放器处于有效的状态以进行搜寻。

   有效状态为“已准备”、“完成”、“已暂停”和“正在播放”。

1. 使用本机SeekBar设置 `OnSeekBarChangeListener` 以查看用户何时进行清理。
1. 收听 `QOSEventListener.onOperationFailed` 并采取相应的措施。

   此事件会传递相应的警告。 您的应用程序决定如何继续，例如，通过再次尝试搜寻或从上一个位置继续播放。

1. 等待TVSDK调用 `QOSEventListener.onSeekComplete` 回调。
1. 使用回调的位置参数检索最终调整的播放位置。

   这很重要，因为搜寻之后的实际开始位置可能与请求的位置不同。 如果搜寻或其他重新定位在广告时间中间结束或跳过广告时间，则播放行为可能会受到影响。

1. 显示搜寻拖移栏时使用位置信息。

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**搜寻示例**

在此示例中，用户擦除搜寻栏以搜寻到所需的位置。

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
