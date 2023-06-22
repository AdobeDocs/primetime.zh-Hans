---
description: TVSDK支持在视频点播(VOD)和实时流中搜索流是滑动窗口播放列表的特定位置（时间）。
title: 显示具有当前播放位置的搜寻清理栏
exl-id: d5bc3a54-7dfd-435e-abb4-323639732e0a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 显示具有当前播放位置的搜寻清理栏 {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支持在视频点播(VOD)和实时流中搜索流是滑动窗口播放列表的特定位置（时间）。

>[!TIP]
>
>只有DVR才允许在实时流中进行搜寻。

1. 设置用于搜寻的回调。

   搜索是异步执行的，因此TVSDK会调度以下与搜索相关的事件：

   * `MediaPlayerEvent.SEEK_BEGIN`，开始搜寻。
   * `MediaPlayerEvent.SEEK_END`，搜寻成功。
   * `MediaPlayerEvent.OPERATION_FAILED`，其中搜寻失败。

1. 等待播放器处于有效的状态以进行搜寻。

   有效状态为“准备”、“完成”、“暂停”和“正在播放”。
1. 使用本机 `SeekBar` 要设置 `OnSeekBarChangeListener`，确定用户何时进行清理。
1. 将请求的搜寻位置（毫秒）传递给 `MediaPlayer.seek` 方法。

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   您只能在资产的可搜索持续时间内查找。 对于点播视频，该值介于0和资产持续时间之间。

   >[!TIP]
   >
   >此步骤将播放头移动到流中的新位置，但最终计算位置可能与指定的搜寻位置不同。

1. 聆听 `MediaPlayerEvent.OPERATION_FAILED` 并采取适当的措施。

   此事件传递相应的警告。 您的应用程序将决定如何继续，选项包括再次尝试搜寻或从上一个位置继续播放。

1. 等待TVSDK调用 `MediaPlayerEvent.SEEK_END` 回调。
1. 使用回调的位置参数检索最终调整的播放位置。

   这很重要，因为搜寻后的实际开始位置可能与请求位置不同。 如果搜寻或其他重新定位在广告时间中间结束或跳过广告时间时，规则（包括播放行为）可能会受到影响。

1. 显示搜寻拖移栏时使用位置信息。

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**搜索示例**

在此示例中，用户擦除搜寻栏以搜寻到所需的位置。

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
