---
description: 当播放到达广告中断、通过广告中断或以广告中断结束时，TVSDK为当前播放头的定位定义了一些默认行为。
title: 使用广告自定义播放
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---


# 使用广告自定义播放{#customize-playback-with-ads}

当播放到达广告中断、通过广告中断或以广告中断结束时，TVSDK为当前播放头的定位定义了一些默认行为。

>[!TIP]
>
>可以使用`PTAdPolicySelector`类覆盖默认行为。

默认行为会因用户在正常播放期间还是通过在视频中进行搜索而有所不同。

您可以通过以下方式自定义广告播放行为：

* 保存用户停止观看视频的位置，并在将来的会话中在同一位置继续播放。
* 如果向用户显示广告中断，则即使用户寻求新位置，也在几分钟内不显示任何其他广告。
* 如果内容在几分钟后无法播放，则重新启动流或故障转移到同一内容的其他源。

   在故障转移回放会话中，要允许用户跳过广告并恢复到上一个失败位置，您可以禁用前置和/或中置广告。 TVSDK提供了可跳过前置和中置广告的方法。

## 广告播放{#section_296ADE00CFEA40CBA1B46142720D13A5}的API元素

TVSDK提供可用于自定义包含广告的内容的播放行为的类和方法。
以下API元素对于自定义播放很有用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API元素 </th> 
   <th colname="col2" class="entry"> 支持广告的内容 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata  </span> </td> 
   <td colname="col2"> 控制是否应将广告中断标记为已被查看者观看，如果是，何时标记。 使用<span class="codeph"> adBreakAsWatched </span>属性设置和获取监视策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector  </span> </td> 
   <td colname="col2"> 允许自定义TVSDK广告行为的协议。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector  </span> </td> 
   <td colname="col2"> 实现默认TVSDK行为的类。 您的应用程序可以覆盖此类，以自定义默认行为，而无需实现完整的界面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer  </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime  </span>。 <p>这是播放的本地时间，不包括已放置广告中断。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime  </span> 。 <p>此处，搜索相对于流中的本地时间发生。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime  </span>。 <p>时间轴上的虚拟位置将转换为本地位置。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak  </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched </span> 属性。指示查看器是否已观看该广告。 </td> 
  </tr> 
 </tbody> 
</table>

## 设置自定义播放{#section_8209BAACC7814C9399988DC7DE9CF4CA}

在可以自定义或覆盖广告行为之前，请使用TVSDK注册广告策略实例。

要自定义广告行为，请执行以下操作之一：

* 符合`PTAdPolicySelector`协议并实现所有必需的策略选择方法。

   如果您需要覆盖&#x200B;**all**&#x200B;默认广告行为，建议使用此选项。

* 覆盖`PTDefaultAdPolicySelector`类，并仅为那些需要自定义的行为提供实现。

   如果只需要覆盖默认行为的&#x200B;**some**，则建议使用此选项。

对于这两个选项，请完成以下任务:

1. 通过客户端工厂注册TVSDK要使用的策略实例。

   >[!NOTE]
   >
   >取消分配`PTMediaPlayer`实例时，将清除在播放开始处注册的自定义广告策略。 每次创建新的播放会话时，应用程序必须注册一个策略选择器实例。

   例如：

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 实施您的自定义。

## 跳过一段时间{#section_99809BE4D9BB4DEEBBF596C746CA428A}的广告中断

默认情况下，TVSDK在用户搜索广告时强制播放广告中断。 如果上一个中断完成所经过的时间在特定分钟内，则可以自定义该行为以跳过广告中断。

>[!IMPORTANT]
>
>当内部搜索跳过广告时，播放时可能稍微暂停。

以下自定义广告策略选择器示例在用户观看广告中断后的五分钟（观看时钟）内跳过广告。

1. 通过客户端工厂注册TVSDK要使用的策略实例。

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 实施您的自定义。

**PTS5MinuteSkipBreakPolicySelector.h**

```
#import "PTMediaPlayerNotifications.h" 
#import "PTMediaPlayer.h" 
#import "PTDefaultAdPolicySelector.h" 
 
//  extend the default policy  
selector@interface PTS5MinuteSkipBreakPolicySelector : PTDefaultAdPolicySelector 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player; 
  
@end
```

**PTS5MinuteSkipBreakPolicySelector.m**

```
#import "PTS5MinuteSkipBreakPolicySelector.h" 
  
double MIN_BREAK_INTERVAL  = 60 * 5; // 5 minutes 
  
@implementation PTS5MinuteSkipBreakPolicySelector 
{ 
    PTMediaPlayer *_player; 
    NSTimeInterval _lastAdBreakPlayedTime; 
} 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player 
{ 
    if (self = [super init]) 
    { 
        _lastAdBreakPlayedTime = 0; 
        _player = [player retain]; 
        [self addobservers]; 
    } 
    
    return self; 
} 
  
- (NSArray *)selectAdBreaksToPlay:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectAdBreaksToPlay (%f): %f", self,  
        CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectAdBreaksToPlay:info]; 
    } 
    
    return nil; 
} 
  
- (PTAdBreakPolicyType)selectPolicyForAdBreak:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectPolicyForAdBreak (%f): %f  %f", self,  
            CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime,  
            [[NSDate date] timeIntervalSince1970]); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectPolicyForAdBreak:info]; 
    } 
    
    return PTAdBreakPolicyTypeSkip; 
} 
  
- (BOOL)shouldPlayAdBreaks 
{ 
    NSTimeInterval currentTime = [[NSDate date] timeIntervalSince1970]; 
    if (_lastAdBreakPlayedTime <= 0) 
    { 
        return YES; 
    } 
    
    if (_lastAdBreakPlayedTime > 0 && (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) 
    { 
        return YES; 
    } 
    
    // don't play any ad break if 5 minutes hasn't elapsed 
    return NO; 
} 
  
- (void) onMediaPlayerAdBreakStarted:(NSNotification *) notification 
{ 
    NSLog(@"%@ - AdBreak Start", self); 
} 
  
- (void) onMediaPlayerAdBreakCompleted:(NSNotification *) notification 
{ 
    _lastAdBreakPlayedTime = [[NSDate date] timeIntervalSince1970]; 
    NSLog(@"%@ - AdBreak Complete at: %f", self, _lastAdBreakPlayedTime); 
} 
  
- (void)addobservers 
{ 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakStarted:)  
                name:PTMediaPlayerAdBreakStartedNotification object:_player]; 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakCompleted:)  
                name:PTMediaPlayerAdBreakCompletedNotification object:_player]; 
} 
  
- (void)removeObservers 
{ 
    [[NSNotificationCenter defaultCenter] removeObserver:self]; 
} 
  
- (void)dealloc 
{ 
    [self removeObservers]; 
    [_player release]; 
    [super dealloc]; 
} 
  
@end
```

## 保存视频位置并稍后恢复{#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

您可以在视频中保存当前播放位置，并在将来的会话中在相同位置继续播放。

动态插入的广告在用户会话之间有所不同，因此将位置&#x200B;**与**&#x200B;拼接的广告保存后，将在将来会话中的位置不同。 TVSDK提供方法来检索播放位置，同时忽略拼接的广告。

1. 当用户退出视频时，您的应用程序将检索并保存视频中的位置。

   >[!TIP]
   >
   >不包括广告期。

   由于广告模式、频率限制等原因，每个会话中的广告中断可能会有所不同。 在将来的会话中，视频在一个会话中的当前时间可能有所不同。 在视频中保存位置时，应用程序会检索本地时间。 使用`localTime`属性读取此位置，可将该位置保存在设备上或服务器上的数据库中。

   例如，如果用户在视频的第20分钟，且此位置包含5分钟广告，则`currentTime`将为1200秒，而此位置的`localTime`将为900秒。

   >[!IMPORTANT]
   >
   >实时/线性流的本地时间和当前时间相同。 在这种情况下，`convertToLocalTime`不起作用。 对于VOD，播放广告时本地时间保持不变。

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
       CMTimeRange seekableRange = self.player.seekableRange; 
   
       if (CMTIMERANGE_IS_VALID(seekableRange)) { 
           double seekableRangeStart = CMTimeGetSeconds(seekableRange.start); 
           double seekableRangeDuration = CMTimeGetSeconds(seekableRange.duration); 
           double currentTime = CMTimeGetSeconds(self.player.currentTime); // includes ads 
           double localTime = CMTimeGetSeconds(self.player.localTime); // no ads 
       } 
   }
   ```

1. 要在同一位置恢复视频，请执行以下操作：要从从上一会话中保存的位置继续播放视频，请使用`seekToLocalTime`

   >[!TIP]
   >
   >只使用本地时间值调用此方法。 如果使用当前时间结果调用该方法，则会发生错误行为。

   要查找当前时间，请使用`seekToTime`。

1. 当应用程序收到`PTMediaPlayerStatusReady`状态更改事件时，请查找保存的本地时间。

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. 按照广告策略接口中的指定提供广告中断。
1. 通过扩展默认广告策略选择器来实施自定义广告策略选择器。
1. 通过实施`selectAdBreaksToPlay`提供必须向用户显示的广告中断

   >[!NOTE]
   >
   >该方法包括在本地时间位置之前的前卷广告中断和中间广告中断。 您的应用程序可以决定播放前置广告中断，并恢复到指定的本地时间，播放中间广告中断，恢复到指定的本地时间，或者不播放广告中断。

