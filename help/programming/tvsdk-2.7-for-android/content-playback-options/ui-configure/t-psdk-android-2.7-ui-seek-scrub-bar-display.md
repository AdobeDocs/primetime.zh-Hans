---
description: TVSDK支持在视频点播(VOD)和直播流中搜索流是滑动窗口播放列表的特定位置（时间）。
seo-description: TVSDK支持在视频点播(VOD)和直播流中搜索流是滑动窗口播放列表的特定位置（时间）。
seo-title: 显示具有当前播放位置的搜索滑动条
title: 显示具有当前播放位置的搜索滑动条
uuid: df045a10-8d74-4874-8fa5-7e9571c8678d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# 显示当前播放位置{#display-a-seek-scrub-bar-with-the-current-playback-position}的搜索滑动条

TVSDK支持在视频点播(VOD)和直播流中搜索流是滑动窗口播放列表的特定位置（时间）。

>[!TIP]
>
>在实时流中搜索仅允许DVR。

1. 设置搜索回呼。

       搜索是异步的，因此TVSDK将分派以下搜索相关事件:
   
   * `MediaPlayerEvent.SEEK_BEGIN`，在那里寻找开始。
   * `MediaPlayerEvent.SEEK_END`，其中搜索成功。
   * `MediaPlayerEvent.OPERATION_FAILED`，其中搜索失败。

1. 等待播放器处于有效状态进行搜索。

   有效状态包括PREPARED、COMPLETE、PAUSED和PLAYING。
1. 使用本机`SeekBar`设置`OnSeekBarChangeListener`，它确定用户何时划动。
1. 将请求的搜索位置（毫秒）传递给`MediaPlayer.seek`方法。

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   您只能在资产的可搜索持续时间内进行搜索。 对于视频点播，即从0到资产持续时间。

   >[!TIP]
   >
   >此步骤将播放头移动到流中的新位置，但最终计算位置可能与指定的搜索位置不同。

1. 侦听`MediaPlayerEvent.OPERATION_FAILED`并采取适当的操作。

   此事件会传递相应的警告。 您的应用程序决定如何继续，这些选项包括再次尝试搜索或从上一位置继续播放。

1. 等待TVSDK调用`MediaPlayerEvent.SEEK_END`回调。
1. 使用回调的位置参数检索最终调整的播放位置。

   这很重要，因为搜索后的实际开始位置可能与请求的位置不同。 如果搜索或其他重新定位在广告中间结束或跳过广告中间，则可能适用规则（包括播放行为）。

1. 在显示搜索拖拽栏时使用位置信息。

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**搜索示例**

在此示例中，用户将搜索条擦到所需位置。

```java
//Use the native SeekBar to set an OnSeekBarChangeListener to 
// see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) { 
            // Update the seek bar thumb with the position provided by the user. 
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

