---
description: 您可以使用TVSDK检索有关播放器在媒体中的位置的信息，并在搜索栏上显示该信息。
seo-description: 您可以使用TVSDK检索有关播放器在媒体中的位置的信息，并在搜索栏上显示该信息。
seo-title: 显示视频的持续时间、当前时间和剩余时间
title: 显示视频的持续时间、当前时间和剩余时间
uuid: 13627fa2-8cd8-4336-bc4b-7e3226330389
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 显示视频的持续时间、当前时间和剩余时间 {#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK检索有关播放器在媒体中的位置的信息，并在搜索栏上显示该信息。

1. 等待播放器至少处于PREPARED状态。
1. 使用该方法检索当前播放头时 `MediaPlayer.getCurrentTime` 间。

   这将返回虚拟时间轴上的当前播放头位置（以毫秒为单位）。 时间是相对于可能包含多个替代内容实例的已解析流计算的，例如连接到主流中的多个广告或广告分段。 对于实时／线性流，返回的时间始终在播放窗口范围内。

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. 检索流的播放范围并确定持续时间。
   1. 使用该 `MediaPlayer.getPlaybackRange` 方法获取虚拟时间线时间范围。

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. 使用该 `MediaPlayer.getPlaybackRange` 方法获取虚拟时间线时间范围。

      * 对于VOD，范围始终以零开头，并且结束值等于主内容持续时间和流（广告）中其他内容的持续时间之和。
      * 对于线性／实时资产，该范围表示播放窗口范围。 播放时，此范围会发生更改。

         TVSDK调用回 `ITEM_Updated` 调以指示媒体项已刷新，并且其属性（包括播放范围）已更新。

1. 使用Android SDK中类 `MediaPlayer` 和类上 `SeekBar` 可用的方法设置搜索栏参数。

   例如，此处是一个可能的布局，它包含搜索栏和两个 `TextView` 元素。

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

1. 使用计时器定期检索当前时间并更新搜索栏，如图所示：

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width=&quot;477.000pt&quot;}

   以下示例使用 `Clock.java` helper类(在中可用 `ReferencePlayer`)作为计时器。 此类设置事件监听器并每秒触发一 `onTick` 个事件，或者触发您可以指定的另一个超时值。

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

   在每个时钟点上，此示例检索媒体播放器的当前位置并更新搜索栏。 它使用两个元 `TextView` 素将当前时间和播放范围结束位置标记为数字值。

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

