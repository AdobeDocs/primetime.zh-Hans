---
description: 您可以使用TVSDK检索可在搜寻栏上显示的媒体信息。
title: 显示视频的持续时间、当前时间和剩余时间
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 显示视频的持续时间、当前时间和剩余时间{#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK检索可在搜寻栏上显示的媒体信息。

1. 等待播放器处于“已准备”状态。
1. 使用检索当前播放头时间 `MediaPlayer.getCurrentTime` 方法。

   这将返回虚拟时间轴上的当前播放头位置（以毫秒为单位）。 所计算的时间相对于解析流而言可能包含替代内容的多个实例，例如连接到主流的多个广告或广告时间。 对于实时/线性流，返回的时间始终在播放窗口范围内。

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. 检索流的播放范围并确定持续时间。
   1. 使用 `mediaPlayer.getPlaybackRange` 方法获取虚拟时间轴的时间范围。

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. 使用以下方式解析时间范围 `mediacore.utils.TimeRange`.
   1. 要确定持续时间，请从范围的末尾减去开始时间。

      这包括插入到流（广告）中的附加内容的持续时间。

      对于VOD，范围始终从零开始，并且结束值等于主内容持续时间与插入到流（广告）中的其他内容的持续时间之和。

      对于线性/实时资源，范围表示播放窗口范围，此范围在播放期间会更改。

      TVSDK调用您的 `onUpdated` 回调，指示媒体项目已刷新并且其属性（包括播放范围）已更新。

1. 使用上的可用方法 `MediaPlayer` 和 `SeekBar` 在Android SDK中公开可用以设置搜寻栏参数的类。

   例如，下面是一个可能的布局，其中包含 `SeekBar` 和两个 `TextView` 元素。

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

1. 使用计时器定期检索当前时间并更新SeekBar。

   以下示例使用 `Clock.java` helper类作为计时器，该计时器可在引用播放器PrimetimeReference中使用。 此类设置事件侦听器，并触发 `onTick` 每秒发生一次的事件，或您可以指定的另一个超时值。

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
   @Override 
   public void onTick(String name) { 
       // Timer event is received. Update the SeekBar here. 
   } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   在每个时钟刻度上，此示例检索媒体播放器的当前位置并更新SeekBar。 它使用两个TextView元素将当前时间和播放范围结束位置标记为数字值。

   ```java
   @Override 
   public void onTick(String name) { 
   if (mediaPlayer != null && mediaPlayer.getStatus() == PlayerState.PLAYING) { 
       handler.post(new Runnable() { 
           @Override 
           public void run() { 
               seekBar.setProgress((int)  
                    mediaPlayer.getCurrentTime()); 
               currentTimeText.setText(timeStampToText( 
                  mediaPlayer.getCurrentTime())); 
               totalTimeText.setText(timeStampToText( 
                   mediaPlayer.getPlaybackRange().getEnd())); 
           } 
       }); 
   } 
   }
   ```
