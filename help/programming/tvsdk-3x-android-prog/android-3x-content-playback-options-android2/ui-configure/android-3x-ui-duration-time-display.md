---
description: 您可以使用TVSDK检索有关播放器在媒体中的位置的信息，并在搜寻栏中显示该信息。
title: 显示视频的持续时间、当前时间和剩余时间
exl-id: 68501c81-346a-4c3e-aa20-a98b8b1c6b17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# 显示视频的持续时间、当前时间和剩余时间 {#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK检索有关播放器在媒体中的位置的信息，并在搜寻栏中显示该信息。

1. 等待播放器至少处于“已准备”状态。
1. 使用检索当前播放头时间 `MediaPlayer.getCurrentTime` 方法。

   这将返回虚拟时间轴上的当前播放头位置（以毫秒为单位）。 计算的时间相对于已解析的流（可能包含替代内容的多个实例，例如拼接到主流的多个广告或广告插播）。 对于实时/线性流，返回的时间始终在播放窗口范围内。

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. 检索流的播放范围并确定持续时间。
   1. 使用 `MediaPlayer.getPlaybackRange` 方法获取虚拟时间轴的时间范围。

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. 使用 `MediaPlayer.getPlaybackRange` 方法获取虚拟时间轴的时间范围。

      * 对于VOD，范围始终从零开始，并且结束值等于主内容持续时间与流（广告）中其他内容的持续时间的总和。
      * 对于线性/实时资源，范围表示播放窗口范围。 此范围在播放期间更改。

         TVSDK调用 `ITEM_Updated` 回调表示媒体项目已刷新，并且其属性（包括播放范围）已更新。

1. 使用以下位置提供的方法： `MediaPlayer` 并在 `SeekBar` 类，用于设置搜寻栏参数。

   例如，下面是一个可能的布局，该布局包含搜寻栏和两个 `TextView` 元素。

   ```xml
   <LinearLayout 
    android:id="@+id/controlBarLayout" 
    android:layout_width="match_parent" 
    android:layout_height="wrap_content" 
    android:layout_alignParentBottom="true" 
    android:background="@android:color/black" 
    android:orientation="horizontal" > 
    <TextView 
       android:id="@+id/playerCurrentTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
    <SeekBar 
       android:id="@+id/playerSeekBar" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_weight="1" /> 
    <TextView 
       android:id="@+id/playerTotalTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
   </LinearLayout>
   ```

1. 使用计时器定期检索当前时间并更新搜寻栏，如下图所示：

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width="477.000pt"}

   以下示例使用 `Clock.java` 帮助程序类，可在 `ReferencePlayer`，作为计时器。 此类设置事件侦听器，并触发 `onTick` 事件间隔，或您可以指定的另一个超时值。

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           // Timer event is received. Update the seek bar here. 
       } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   在每个时钟滴答中，此示例检索媒体播放器的当前位置并更新搜寻栏。 它使用两个 `TextView` 元素，用于将当前时间和播放范围结束位置标记为数值。

   ```java
   @Override 
   public void onTick(String name) { 
       if (mediaPlayer != null &&  
         mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
           handler.post(new Runnable() { 
               @Override 
               public void run() { 
                   seekBar.setProgress((int) mediaPlayer.getCurrentTime()); 
                   currentTimeText.setText(timeStampToText(mediaPlayer.getCurrentTime())); 
                   totalTimeText.setText(timeStampToText(mediaPlayer.getPlaybackRange().getEnd())); 
               } 
           }); 
       } 
   } 
   ```
