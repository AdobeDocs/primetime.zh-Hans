---
description: 您可以使用TVSDK检索可在搜索栏上显示的媒体的相关信息。
seo-description: 您可以使用TVSDK检索可在搜索栏上显示的媒体的相关信息。
seo-title: 显示视频的持续时间、当前时间和剩余时间
title: 显示视频的持续时间、当前时间和剩余时间
uuid: afb43169-2d82-4137-ba38-27caef3d8c21
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# 显示视频的持续时间、当前时间和剩余时间{#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK检索可在搜索栏上显示的媒体的相关信息。

1. 等待您的播放器处于PREPARED状态。
1. 使用`MediaPlayer.getCurrentTime`方法检索当前播放头时间。

   这将返回虚拟时间线上的当前播放头位置（以毫秒为单位）。 时间是相对于可能包含多个替代内容实例的已解析流计算的，例如，将多个广告或广告片段拼接到主流中。 对于实时／线性流，返回的时间始终在播放窗口范围内。

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. 检索流的播放范围并确定持续时间。
   1. 使用`mediaPlayer.getPlaybackRange`方法获取虚拟时间线时间范围。

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. 使用`mediacore.utils.TimeRange`分析时间范围。
   1. 要确定持续时间，请从范围末尾减去开始。

      这包括插入到流中的其他内容的持续时间（广告）。

      对于VOD，范围始终以零开头，并且结束值等于在流（广告）中插入的主内容持续时间和附加内容的持续时间之和。

      对于线性／实时资产，该范围表示播放窗口范围，且该范围在播放过程中会发生变化。

      TVSDK调用您的`onUpdated`回调，以指示媒体项已刷新，并且其属性（包括播放范围）已更新。

1. 使用Android SDK中公开的`MediaPlayer`和`SeekBar`类上可用的方法设置搜索栏参数。

   例如，下面是一个可能的布局，它包含`SeekBar`和两个`TextView`元素。

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

   以下示例使用`Clock.java`帮助程序类作为计时器，该计时器在参考播放器PrimetimeReference中可用。 此类设置事件监听器并每秒触发一个`onTick`事件，或触发您可以指定的另一个超时值。

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

   此示例在每个时钟点上检索媒体播放器的当前位置并更新SeekBar。 它使用两个TextView元素将当前时间和播放范围结束位置标记为数值。

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

