---
description: 当播放到达广告时间、经过广告时间或结束广告时间时，TVSDK会为当前播放头的位置定义一些默认行为。
title: 使用广告自定义播放
exl-id: 522f0b55-dcc4-4175-91ab-757b72bbad23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---

# 使用广告自定义播放 {#customize-playback-with-ads}

当播放到达广告时间、经过广告时间或结束广告时间时，TVSDK会为当前播放头的位置定义一些默认行为。

>[!TIP]
>
>您可以使用覆盖默认行为 `PTAdPolicySelector` 类。

默认行为会有所不同，具体取决于用户是在正常播放期间还是通过在视频中搜寻来传递广告时间。

您可以通过以下方式自定义广告播放行为：

* 保存用户停止观看视频的位置，并在未来会话的同一位置恢复播放。
* 如果将广告时间呈现给用户，那么在几分钟内不显示任何其他广告，即使用户寻求新位置。
* 如果内容在几分钟后无法播放，请重新启动流或故障转移到相同内容的其他源。

   在故障转移播放会话上，要允许用户跳过广告并继续到上一个失败位置，您可以禁用前置广告和/或中置广告。 TVSDK提供了启用跳过前置广告和中置广告的方法。

## 用于广告播放的API元素 {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK提供了可用于自定义包含广告的内容播放行为的类和方法。
以下API元素对于自定义播放非常有用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>API元素</b></th> 
   <th colname="col2" class="entry"><b>支持广告的内容</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata </span> </td> 
   <td colname="col2"> 控制是否应将广告时间标记为已观看者观看，如果是，则何时将其标记为已观看。 使用设置并获取受监视的策略 <span class="codeph"> adBreakAsWatched </span> 属性。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ptadPolicySelector </span> </td> 
   <td colname="col2"> 允许自定义TVSDK广告行为的协议。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> 实现默认TVSDK行为的类。 您的应用程序可以覆盖此类以自定义默认行为，而无需实现完整的接口。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>. <p>这是播放的本地时间，不包括置入的广告时间。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> . <p>在此处，搜寻相对于流中的本地时间进行。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>. <p>时间轴上的虚拟位置被转换为本地位置。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched </span> 属性。 指示查看器是否观看了广告。 </td> 
  </tr> 
 </tbody> 
</table>

## 设置自定义播放 {#section_8209BAACC7814C9399988DC7DE9CF4CA}

在自定义或覆盖广告行为之前，请使用TVSDK注册广告策略实例。

要自定义广告行为，请执行以下操作之一：

* 符合 `PTAdPolicySelector` 协议和实现所有需要的策略选择方法。

   如果需要覆盖，建议使用此选项 **所有** 默认广告行为。

* 覆盖 `PTDefaultAdPolicySelector` 类，并仅为那些需要自定义的行为提供实现。

   如果您只需要覆盖，则建议使用此选项 **部分** 缺省行为的URL值。

对于这两个选项，请完成以下任务：

1. 通过客户端工厂注册TVSDK要使用的策略实例。

   >[!NOTE]
   >
   >在播放开始时注册的自定义广告策略在以下情况下被清除： `PTMediaPlayer` 实例已取消分配。 每次创建新播放会话时，您的应用程序都必须注册一个策略选择器实例。

   例如：

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 实施您的自定义项。

## 跳过一段时间的广告时间 {#section_99809BE4D9BB4DEEBBF596C746CA428A}

默认情况下，当用户搜寻广告时间时，TVSDK会强制播放广告时间。 如果距上一个广告时间完成的时间在某个分钟数内，您可以自定义跳过广告时间的行为。

>[!IMPORTANT]
>
>当存在跳过广告的内部搜寻时，播放中可能会稍微暂停。

以下自定义广告策略选择器的示例在用户观看广告时间后五分钟（墙上时钟时间）内跳过广告。

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

## 保存视频位置并稍后恢复 {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

您可以将当前播放位置保存在视频中，并在未来会话中恢复在同一位置播放。

动态插入的广告在用户会话之间有所不同，因此保存了位置 **替换为** 拼接广告是指将来会话中的不同位置。 TVSDK提供了在忽略拼接广告时检索播放位置的方法。

1. 当用户退出视频时，您的应用程序将检索并保存视频中的位置。

   >[!TIP]
   >
   >不包括广告持续时间。

   由于广告模式、频率上限等等，每个会话中的广告时间可能会有所不同。 一个会话中视频的当前时间可能会与将来会话中的不同。 在视频中保存位置时，应用程序检索本地时间。 使用  `localTime` 属性来读取此位置，您可以将其保存在设备上或服务器上的数据库中。

   例如，如果用户位于视频的第20分钟，并且此位置包含五分钟的广告， `currentTime` 为1200秒，而 `localTime` 在此位置将为900秒。

   >[!IMPORTANT]
   >
   >对于实时/线性流，本地时间和当前时间相同。 在这个案例中， `convertToLocalTime` 没有效果。 对于VOD，播放广告时本地时间保持不变。

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

1. 要在上一个会话中保存的相同位置恢复视频，请使用 `seekToLocalTime`.

   >[!TIP]
   >
   >仅使用本地时间值调用此方法。 如果使用当前时间结果调用方法，则会发生错误行为。

   要搜索到当前时间，请使用 `seekToTime`.

1. 当您的应用程序收到 `PTMediaPlayerStatusReady` 状态更改事件，搜索到保存的本地时间。

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. 提供广告策略界面中指定的广告时间。
1. 通过扩展默认的广告策略选择器，实施自定义广告策略选择器。
1. 通过实施，提供必须呈现给用户的广告时间 `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >此方法包括前置广告时间和中置广告时间位于本地时间位置之前。 您的应用程序可以决定播放前置广告时间并继续到指定的本地时间，播放中置广告时间并继续到指定的本地时间，或者不播放任何广告时间。
