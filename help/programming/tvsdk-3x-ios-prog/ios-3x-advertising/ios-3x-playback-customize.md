---
description: 当播放到达广告中断、传递广告中断或以广告中断结束时，TVSDK为当前播放头的位置定义一些默认行为。
seo-description: 当播放到达广告中断、传递广告中断或以广告中断结束时，TVSDK为当前播放头的位置定义一些默认行为。
seo-title: 使用广告自定义播放
title: 使用广告自定义播放
uuid: b21a2b1b-5376-41cb-a772-a8945fd56f3c
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 使用广告自定义播放 {#customize-playback-with-ads}

当播放到达广告中断、传递广告中断或以广告中断结束时，TVSDK为当前播放头的位置定义一些默认行为。

>[!TIP]
>
>可以使用类覆盖默认行 `PTAdPolicySelector` 为。

默认行为因用户在正常播放期间还是通过在视频中进行搜索而异。

您可以通过以下方式自定义广告播放行为：

* 保存用户停止观看视频的位置，并在将来的会话中在同一位置继续播放。
* 如果向用户展示广告中断，则在数分钟内不会显示任何其他广告，即使用户寻求新位置也是如此。
* 如果内容在几分钟后无法播放，请重新启动流，或为同一内容故障切换到其他源。

   在故障转移回放会话中，要允许用户跳过广告并恢复到上一个失败位置，您可以禁用前置和／或中置广告。 TVSDK提供了跳过前置和中置广告的方法。

## 用于广告播放的API元素 {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK提供了类和方法，您可以使用它们自定义包含广告的内容的播放行为。
以下API元素对于自定义播放很有用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>API元素</b></th> 
   <th colname="col2" class="entry"><b>支持广告的内容</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAd元数据 </span> </td> 
   <td colname="col2"> 控制广告分时段是否应标记为已被查看者观看，如果是，何时标记。 使用adBreakAsWatched属性设置和获取 <span class="codeph"> 监视策 </span> 略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector </span> </td> 
   <td colname="col2"> 允许自定义TVSDK广告行为的协议。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> 实现默认TVSDK行为的类。 应用程序可以覆盖此类，以自定义默认行为，而无需实现完整的界面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>。 <p>这是播放的本地时间，不包括已放置的广告中断。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> 。 <p>此处，搜索相对于流中的本地时间进行。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>。 <p>时间轴上的虚拟位置将转换为本地位置。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched属 </span> 性。 指示查看器是否已观看广告。 </td> 
  </tr> 
 </tbody> 
</table>

## 设置自定义播放 {#section_8209BAACC7814C9399988DC7DE9CF4CA}

在自定义或覆盖广告行为之前，请先向TVSDK注册广告策略实例。

要自定义广告行为，请执行以下操作之一：

* 符合协议并 `PTAdPolicySelector` 实现所有必需的策略选择方法。

   如果您需要覆盖所有默认广告 **行为** ，则建议使用此选项。

* 覆盖类 `PTDefaultAdPolicySelector` 并仅为那些需要自定义的行为提供实现。

   如果只需覆盖部分默认行 **为** ，建议使用此选项。

对于这两个选项，请完成以下任务：

1. 通过客户端工厂注册TVSDK要使用的策略实例。

   >[!NOTE]
   >
   >取消分配实例时，将在播放开始时注册的自定义广告策 `PTMediaPlayer` 略将被清除。 每次创建新的播放会话时，应用程序都必须注册一个策略选择器实例。

   例如：

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 实施您的自定义。

## 跳过一段时间的广告中断 {#section_99809BE4D9BB4DEEBBF596C746CA428A}

默认情况下，TVSDK在用户搜索广告中断时强制播放广告中断。 如果从上一个中断完成开始经过的时间在特定的分钟数内，您可以自定义该行为以跳过广告中断。

>[!IMPORTANT]
>
>当有内部搜索跳过广告时，回放中可能会稍微暂停。

以下自定义广告策略选择器的示例在用户观看广告中断后的5分钟内（挂钟时间）跳过广告。

1. 通过客户端工厂注册TVSDK要使用的策略实例。

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. 实施自定义。

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

## 保存视频位置，稍后恢复 {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

您可以保存视频中的当前播放位置，并在将来的会话中在相同位置继续播放。

动态插入的广告在用户会话之间有所不同，因此用拼接的 **广告保存位置** ，是指将来会话中的不同位置。 TVSDK提供了在忽略拼接广告时检索播放位置的方法。

1. 当用户退出视频时，应用程序将检索并保存视频中的位置。

   >[!TIP]
   >
   >不包括广告持续时间。

   由于广告模式、频率限制等原因，每个会话中的广告中断可能会有所不同。 在将来的会话中，视频在一个会话中的当前时间可能不同。 在视频中保存位置时，应用程序将检索本地时间。 使用属 `localTime` 性读取此位置，该位置可保存在设备上或服务器上的数据库中。

   例如，如果用户在视频的第20分钟，且此位置包括5分钟广告，则 `currentTime` 为1200秒，而 `localTime` 此位置为900秒。

   >[!IMPORTANT]
   >
   >实时／线性流的本地时间和当前时间相同。 在这种情况下， `convertToLocalTime` 效果不佳。 对于VOD，播放广告时本地时间保持不变。

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

1. 要在从上一会话保存的同一位置恢复视频，请使用 `seekToLocalTime`。

   >[!TIP]
   >
   >仅使用本地时间值调用此方法。 如果使用当前时间结果调用该方法，则会发生错误行为。

   要寻找当前时间，请使用 `seekToTime`。

1. 当应用程序收到状 `PTMediaPlayerStatusReady` 态更改事件时，请搜索保存的本地时间。

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. 按照广告策略界面中的指定提供广告中断。
1. 通过扩展默认广告策略选择器来实施自定义广告策略选择器。
1. 通过实施 `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >该方法包括在本地时间位置之前的预卷广告中断和中卷广告中断。 您的应用程序可以决定播放前置广告中断并恢复到指定的本地时间，播放中间广告中断并恢复到指定的本地时间，或者不播放广告中断。