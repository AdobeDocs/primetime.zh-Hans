---
description: 当用户快速前进或快速后退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为非1的值。
seo-description: 当用户快速前进或快速后退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为非1的值。
seo-title: 实现快进和后退
title: 实现快进和后退
uuid: c1992757-d067-4c11-8d08-fec09099476f
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---


# 实现快速前进和后退{#implement-fast-forward-and-rewind}

当用户快速前进或快速后退通过媒体时，他们处于特技播放模式。 要进入特技播放模式，您需要将MediaPlayer播放速率设置为非1的值。

>[!IMPORTANT]
>
>* 仅MPEG Dash和HLS VOD内容支持技巧播放模式。
>* 直播流或广告不支持技巧播放模式。
>* 当从主内容切换到广告时，浏览器TVSDK会保留特技播放模式。

>



要切换速度，必须设置一个值。

1. 通过将`MediaPlayer`上的速率设置为允许的值，从正常播放模式(1x)移动到特技播放模式。

   * `MediaPlayerItem`类定义允许的播放速率。
   * 如果不允许指定速率，浏览器TVSDK将选择最接近的允许速率。

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

1. 您可以选择侦听汇率变化事件，这会让您知道您何时请求汇率变化以及实际发生汇率变化的时间。

       浏览器TVSDK调度以下与特技播放相关的事件:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 值变 `rate` 为其他值时。

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 以选定速率恢复播放时。

      当播放器从技巧播放模式返回到正常播放模式时，浏览器TVSDK将调度这两个事件。

## 速率更改API元素{#rate-change-API-elements}

浏览器TVSDK包括确定有效率、当前速率、技巧播放是否受支持以及与快速前进和后退相关的其他功能的方法、属性和事件。

使用以下API元素更改播放率：

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` -指定有效费率。

   | 比率值 | 播放效果 |
   |---|---|
   | 2.0、4.0、8.0、16.0、32.0、64.0 | 切换到快进模式时，指定的乘法器比正常速度快（例如，4比正常速度快4倍） |
   | -2.0、-4.0、-8.0、-16.0、-32.0、-64.0 | 切换到快速后退模式 |
   | 1.0 | 切换为正常播放模式（调用`play`与将速率属性设置为1.0相同） |
   | 0.0 | 暂停（调用`pause`与将速率属性设置为0.0相同） |

## 技巧播放{#limitations-and-behavior-trick-play}的限制和行为

技巧播放模式的行为方式存在一些限制和问题。

以下是技巧播放模式限制的列表:

* 如果流不包含特技播放适配，则禁用快速倒回，并且快进的最大播放速率限制为8。
* 当使用特技播放适配来提供特技模式时，将禁用音轨。
* 在特技播放模式下，禁用音频和隐藏式字幕轨道的切换。
* 播放和暂停已启用。
* 在搜索时，如果播放处于特技播放模式，则播放速率设置为1并恢复正常播放。
* 自适应比特率(ABR)逻辑被启用。

   在使用正常的适应时，用户档案在`ABRControlParameters.minBitRate`和`ABRControlParameters.maxBitRate`之间受到限制。 在使用特技播放改编时，用户档案在`ABRControlParameters.minTrickPlayBitRate`和`ABRControlParameters.maxTrickPlayBitRate`之间受限。