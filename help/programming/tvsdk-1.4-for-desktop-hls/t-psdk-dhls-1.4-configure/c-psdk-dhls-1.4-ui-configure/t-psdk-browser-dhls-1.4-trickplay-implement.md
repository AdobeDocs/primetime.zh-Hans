---
description: 当用户快速前进或快速后退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为非1的值。
title: 实现快进和后退
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---


# 实现快进和后退{#implement-fast-forward-and-rewind}

当用户快速前进或快速后退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为非1的值。

要切换速度，必须设置一个值。

1. 通过将`MediaPlayer`上的`rate`属性设置为允许的值，从正常播放模式(1x)移动到特技播放模式。

   * `MediaPlayerItem`类定义允许的播放速率。
   * 如果不允许指定速率，TVSDK将选择最接近的允许速率。

      当滴播速率从0（暂停）或1（正常播放）更改为大于1或小于–1的速率时，将删除时间轴上的所有广告。 整个时间线上只有一个时段，可促进一个变戏法动作，使内容可以快速转发和重新绕排，而无需停在任何广告位置。 此操作由TVSDK上的时间轴拆离操作启用，以删除所有已解析的adBreaks。 当trickplay在0或1恢复时，adBreaks首先由时间轴附件操作恢复。

      请记住以下信息：

   * 如果特技播放动作是倒回内容，则当速率更改为1时，将继续播放。
   * 如果要快速前进内容，则上次跳过的adBreak会在恢复位置播放。

   此示例将播放器的内部播放速率设置为请求的速率。

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. 您可以选择侦听汇率变化事件，这会让您知道何时请求汇率变化以及实际发生汇率变化的时间。

   TVSDK调度以下与特技播放相关的事件:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` 值变 `rate` 为其他值时。

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` 以选定的速率恢复播放时。

   当播放器从特技播放模式返回到正常播放模式时，TVSDK将调度这两个事件。

## 速率更改API元素{#rate-change-api}

TVSDK包括确定有效率、当前速率、特技播放是否受支持以及与快速前进和后退相关的其他功能的方法、属性和事件。

使用以下API元素更改播放率：

* `MediaPlayer.rate` setter和getter函数的属性
* `MediaPlayer.localTime property` 使用getter函数
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` getter函数的属性
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` getter函数的属性 — 指定有效率。

| 速率值 | 播放效果 |
|---|---|
| 2.0、4.0、8.0、16.0、32.0、64.0、128.0 | 切换到快进模式时，指定的乘数比正常速度快（例如，4比正常速度快4倍） |
| -2.0、-4.0、-8.0、-16.0、-32.0、-64.0、-128.0 | 切换到快速后退模式 |
| 1.0 | 切换到正常播放模式（调用`play`与将rate属性设置为1.0相同） |
| 0.0 | 暂停（调用`pause`与将速率属性设置为0.0相同） |

## 特技播放{#limitations-behavior-trick-play}的限制和行为

下面是技巧播放模式的限制：

* 主控的播放列表必须包含仅限I帧的区段。 屏幕上只显示I帧轨道的关键帧。
* 将禁用音轨和隐藏式字幕。
* 自适应位速率(ABR)逻辑被禁用。 TVSDK在最低提供的速率和800 kbps之间选择一个比特率，并在整个特技播放会话期间使用该速率。
* 播放和暂停已启用。
* 不允许搜索。 要进行搜索，请调用`pause`退出特技播放模式，然后调用`seek`。

* 您可以将特技播放模式退出到任何允许的播放速率（播放或暂停）。
* 在流中加入广告时：

   * 您只能在播放主内容时玩耍。 如果您尝试在广告中断期间切换到特技播放，则会调度错误。
   * 开始特技播放模式后，将忽略广告中断且不会触发广告事件。
   * 即使跳过广告分段，TVSDK向播放器应用程序公开的时间线也不会被修改。
   * `MediaPlayer.currentTime`属性在跳过广告中断的持续时间内向前（快进）或向后（快退）跳转。 当前时间的这种跳转行为允许在特技播放期间保持流持续时间不变。 您的播放器应用程序可以使用`localTime`属性来跟踪相对于主内容的时间。 跳过广告时，不会对本地时间返回的值执行时间跳转。

   * 将在即将跳过广告分段之前立即调度`AdBreakPlaybackEvent.AD_BREAK_SKIPPED`事件。 您的播放器可以使用此事件来实现与跳过的广告中断相关的自定义逻辑。
   * 退出特技播放会调用与退出搜索时相同的广告播放策略。

      因此，与搜索一样，行为取决于应用程序的播放策略是否与默认策略不同。 默认情况是，最后一个跳过的广告中断是在您退出特技播放时播放的。