---
description: 当用户快进或快退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为1以外的值。
title: 实现快速前进和倒带
exl-id: c1d70d46-449b-494b-9b89-5553e9bcdbc3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# 实现快速前进和倒带 {#implement-fast-forward-and-rewind}

当用户快进或快退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为1以外的值。

要切换速度，必须设置一个值。

1. 通过设置，从正常播放模式(1x)移动到特技播放模式 `rate` 上的属性 `MediaPlayer` 到允许的值。

   * 此 `MediaPlayerItem` 类定义允许的播放速率。
   * 如果不允许指定的速率，则TVSDK会选择允许的最接近的速率。

      当点击播放速率从0（暂停）或1（正常播放）更改为大于1或小于–1的速率时，时间轴上的所有广告都将被删除。 在整个时间轴上只有一个句点，这有助于点击播放操作，以允许内容快速转发和倒带，而无需停止在任何广告位置。 此操作由TVSDK上的时间轴分离操作启用，以删除所有已解析的广告符。 在0或1处继续播放时，将首先通过时间轴附件操作恢复adBreak。

      请记住以下信息：

   * 如果点击播放操作是倒带内容，则当播放速率更改为1时，将恢复播放。
   * 如果点击播放操作是快速转发内容，则最后一个跳过的广告时间将在恢复位置播放。

   此示例将播放器的内部播放速率设置为请求的速率。

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. 您可以选择监听速率更改事件，这可以让您知道何时请求速率更改以及何时实际发生速率更改。

   TVSDK调度以下与特技播放相关的事件：

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` 当 `rate` 值会更改为其他值。

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` 以选定的速率继续播放时。

   当播放器从特技播放模式返回到正常播放模式时，TVSDK会调度这两个事件。

## 费率更改API元素 {#rate-change-api}

TVSDK包括用于确定有效速率、当前速率、是否支持特技播放以及与快速前进和倒带相关的其他功能的方法、属性和事件。

使用以下API元素更改播放率：

* `MediaPlayer.rate` 具有setter和getter函数的属性
* `MediaPlayer.localTime property` 使用getter函数
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` 具有getter函数的属性
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` 使用getter函数的属性 — 指定有效速率。

| 费率值 | 对播放的影响 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0  , 128.0 | 使用指定的乘数快速切换到快进模式（例如，4比正常快4倍） |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  , -128.0 | 切换到快速倒带模式 |
| 1.0 | 切换到正常播放模式(呼叫 `play` 与将rate属性设置为1.0相同) |
| 0.0 | 暂停（调用） `pause` 与将rate属性设置为0.0相同) |

## 特技播放的限制和行为 {#limitations-behavior-trick-play}

以下是特技播放模式的限制：

* 主控播放列表必须包含仅限I帧的区段。 屏幕上只显示来自I帧轨道的关键帧。
* 禁用了音轨和隐藏式字幕。
* 自适应比特率(ABR)逻辑已禁用。 TVSDK选择最低提供速率和800 kbps之间的一个比特率，并在整个特技播放会话期间使用该比特率。
* 已启用播放和暂停。
* 不允许搜寻。 要搜寻，请调用 `pause` 退出特技播放模式，然后调用 `seek`.

* 您可以退出特技播放模式，进入任何允许的播放速率（播放或暂停）。
* 将广告合并到流中时：

   * 只有在播放主内容时才能玩特技游戏。 如果您尝试在广告时间切换为特技播放，则会发送错误。
   * 在开始特技播放模式后，广告时间将被忽略，并且不会触发任何广告事件。
   * 即使跳过广告时间，TVSDK向播放器应用程序公开的时间轴也不会被修改。
   * 此 `MediaPlayer.currentTime` 属性会随着跳过的广告时间的持续而前移（在快速前进时）或后退（在快速倒带时）。 当前时间的这种跳转行为允许流持续时间在特技播放期间保持未修改。 您的播放器应用程序可以使用 `localTime` 属性，用于跟踪仅相对于主内容的时间。 跳过广告时，不对返回本地时间值执行时间跳转。

   * 此 `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` 紧接在即将跳过广告时间之前调度事件。 您的播放器可以使用此事件实施与跳过的广告时间相关的自定义逻辑。
   * 退出特技播放调用与退出搜寻时相同的广告播放策略。

      因此，与在搜寻中一样，行为取决于应用程序的播放策略是否与默认策略不同。 默认情况是，在您结束特技播放时播放最后一个跳过的广告时间。
