---
description: 您可以显示正在播放的内容的当前时间和剩余时间。
seo-description: 您可以显示正在播放的内容的当前时间和剩余时间。
seo-title: 显示具有当前播放时间位置的搜索拖拽栏
title: 显示具有当前播放时间位置的搜索拖拽栏
uuid: 3a13f4a5-538d-4e7e-ac24-043927f3f2ee
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# 显示当前播放时间位置{#display-a-seek-scrub-bar-with-the-current-playback-time-position}的搜索滑动条

您可以显示正在播放的内容的当前时间和剩余时间。

要实现划动栏，请使用以下示例代码：

```
// 1. Register for the PTMediaPlayerTimeChangeNotification 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerTimeChange:)  
  name:PTMediaPlayerTimeChangeNotification object:self.player]; 
 
... 
 
_positionSlider = [[UISlider alloc] initWithFrame:CGRectMake(105.0, 14.0, 370, 24)];  
[_positionSlider addTarget:self action:@selector(sliderThumbReleased:)  
  forControlEvents:UIControlEventTouchUpInside]; 
 
... 
 
// 2. Cover the event where the user moves to a different location in the stream 
- (void)sliderThumbReleased:(id)sender { 
    double  sliderTime = [_positionSlider  value];  
    CMTimeRange seekableRange = self.player.seekableRange; 
    if (CMTIMERANGE_IS_VALID(seekableRange)) { 
        double start = CMTimeGetSeconds(seekableRange.start);  
        double duration = CMTimeGetSeconds(seekableRange.duration); 
 
        CMTime newTime = CMTimeMakeWithSeconds((sliderTime * duration) + start, AD_TIMESCALE);  
        [self.player seekToTime:newTime]; 
    } 
} 
 
... 
 
// 3. This method is called whenever the player time changes  
(PTMediaPlayerTimeChangeNotification) 
- (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
    CMTimeRange seekableRange = self.player.seekableRange; 
 
    if (CMTIMERANGE_IS_VALID(seekableRange)) { 
        double start = CMTimeGetSeconds(seekableRange.start);  
        double duration = CMTimeGetSeconds(seekableRange.duration); 
        double currentTime = CMTimeGetSeconds(self.player.currentItem.currentTime); 
 
        if (duration > 0) { 
            //Set the position slider value on the current playback time  
            [_positionSlider setValue:((currentTime - start) / duration)]; 
        } 
    } 
} 
```
