---
description: 当用户快进或快退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为1以外的值。
title: 实施快速前进和倒带
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# 实施快速前进和倒带{#implement-fast-forward-and-rewind}

当用户快进或快退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为1以外的值。

>[!IMPORTANT]
>
>* 仅对MPEG短划线和HLS VOD内容支持特技播放模式。
>* 实时流或广告不支持特技播放模式。
>* 从主内容切换到广告时，浏览器TVSDK会保留特技播放模式。
>

要切换速度，必须设置一个值。

1. 通过设置播放速率，从正常播放模式(1x)切换到特技播放模式。 `MediaPlayer` 到允许的值。

   * 此 `MediaPlayerItem` 类定义允许的播放速率。
   * 如果不允许使用指定的速率，则浏览器TVSDK会选择允许的最接近的速率。

     以下示例函数设置速率：

     ```js
     setTrickPlayRate = function (player, trickPlayRate) { 
                   player.rate = trickPlayRate; 
     }
     ```

     以下示例函数可用于查询可用的播放速率：

     ```js
     getAvailableTrickPlayRates = function (player) { 
              var item = player.currentItem; 
              var availableRates = item. availablePlaybackRates; 
              return availableRates; 
     } 
     ```

1. 您可以选择监听费率更改事件，以便您了解何时请求进行费率更改以及何时实际发生费率更改。

       浏览器TVSDK将调度以下与特技播放相关的事件：
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 当 `rate` 值将更改为其他值。

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 以选定的速率继续播放时。

     当播放器从特技播放模式返回到正常播放模式时，浏览器TVSDK会调度这两个事件。

## 费率更改API元素 {#rate-change-API-elements}

浏览器TVSDK包括用于确定有效速率、当前速率、是否支持特技播放以及与快速前进和倒带相关的其他功能的方法、属性和事件。

使用以下API元素更改播放率：

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates`  — 指定有效费率。

  | 费率值 | 播放效果 |
  |---|---|
  | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | 使用指定的乘数快速切换到快进模式（例如，4比正常快4倍） |
  | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | 切换到快速倒带模式 |
  | 1.0 | 切换到正常播放模式(调用 `play` 与将rate属性设置为1.0相同) |
  | 0.0 | 暂停（调用） `pause` 与将rate属性设置为0.0相同) |

## 特技播放的限制和行为 {#limitations-and-behavior-trick-play}

特技播放模式的行为方式存在一些限制和问题。

以下是特技播放模式限制列表：

* 如果流不包含特技播放适配，则禁用快速倒带，并且快进的最大播放速率限制为8。
* 当特技播放适配用于提供特技模式时，音频轨道被禁用。
* 在特技播放模式中，音频和隐藏字幕轨道的切换被禁用。
* 已启用播放和暂停。
* 在搜寻时，如果播放处于特技播放模式，则播放速率设置为1并继续正常播放。
* 自适应比特率(ABR)逻辑已启用。

  使用普通自适应时，配置文件被限制在 `ABRControlParameters.minBitRate` 和 `ABRControlParameters.maxBitRate`. 当使用特技播放自适应时，配置文件被限制在 `ABRControlParameters.minTrickPlayBitRate` 和 `ABRControlParameters.maxTrickPlayBitRate`.
