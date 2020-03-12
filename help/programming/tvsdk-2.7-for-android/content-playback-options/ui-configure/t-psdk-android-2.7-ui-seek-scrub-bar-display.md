---
description: TVSDK支持搜索到特定位置（时间），在该位置，流是视频点播(VOD)和实时流中的滑动窗口播放列表。
seo-description: TVSDK支持搜索到特定位置（时间），在该位置，流是视频点播(VOD)和实时流中的滑动窗口播放列表。
seo-title: 显示具有当前播放位置的搜索滑动条
title: 显示具有当前播放位置的搜索滑动条
uuid: df045a10-8d74-4874-8fa5-7e9571c8678d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# 显示具有当前播放位置的搜索滑动条 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支持搜索到特定位置（时间），在该位置，流是视频点播(VOD)和实时流中的滑动窗口播放列表。

>[!TIP]
>
>仅DVR允许在实时流中搜索。

1. 设置搜索回调。

       搜索是异步的，因此TVSDK会调度以下与搜索相关的事件：
   
   * `MediaPlayerEvent.SEEK_BEGIN`，搜索开始的位置。
   * `MediaPlayerEvent.SEEK_END`，其中搜索成功。
   * `MediaPlayerEvent.OPERATION_FAILED`，其中搜索失败。

1. 等待播放器处于有效状态进行搜索。

   有效状态包括“PREPARED”（准备）、“COMPLETE”（完成）、“PAUSED”（暂停）和“PLAYING”（正在播放）。
1. 使用本机 `SeekBar` 设置， `OnSeekBarChangeListener`它决定用户何时划动。
1. 将所请求的搜索位置（毫秒）传递到该 `MediaPlayer.seek` 方法。

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   您只能在资产的可搜索持续时间内进行搜索。 对于视频（按需），即从0到资产持续时间。

   >[!TIP]
   >
   >此步骤将播放头移动到流中的新位置，但最终计算的位置可能与指定的搜索位置不同。

1. 倾听并 `MediaPlayerEvent.OPERATION_FAILED` 采取适当的行动。

   此事件会传递相应的警告。 应用程序确定如何继续，这些选项包括再次尝试搜索或从上一个位置继续回放。

1. 等待TVSDK调用回 `MediaPlayerEvent.SEEK_END` 调。
1. 使用回调的位置参数检索最终调整的播放位置。

   这很重要，因为搜索后的实际开始位置可能与请求的位置不同。 如果搜索或其他重新定位在广告中断的中间结束或跳过广告中断，则包括播放行为在内的规则可能会受到影响。

1. 显示搜索拖拽栏时，请使用位置信息。

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**搜索示例**

在此示例中，用户将搜索栏拖动到所需位置。

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

