---
description: 可使用TVSDK检索可在搜索栏上显示的有关媒体的信息。
seo-description: 可使用TVSDK检索可在搜索栏上显示的有关媒体的信息。
seo-title: 显示视频的持续时间、当前时间和剩余时间
title: 显示视频的持续时间、当前时间和剩余时间
uuid: 64536ba7-33a1-49f8-a947-5700e1e9c032
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 显示视频的持续时间、当前时间和剩余时间{#display-the-duration-current-time-and-remaining-time-of-the-video}

可使用TVSDK检索可在搜索栏上显示的有关媒体的信息。

1. 等待播放器处于“已初始化”状态。
1. 使用属性检索当前播放头 `MediaPlayer.currentTime` 时间。

   这将返回虚拟时间线上的当前播放头位置（以毫秒为单位）。 时间是相对于可能包含多个替代内容实例的已解析流计算的，例如连接到主流中的多个广告或广告分段。 对于实时／线性流，返回的时间始终在播放窗口范围内。

   ```
   function get currentTime():Number;
   ```

1. 检索流的播放范围并确定持续时间。
   1. 使用该 `mediaPlayer.playbackRange` 属性可获取虚拟时间线时间范围。

      ```
      function get playbackRange():TimeRange;
      ```

   1. 使用解析时间范围 `mediacore.utils.TimeRange`。
   1. 要确定持续时间，请从范围末尾减去开始。

      这包括插入到流（广告）中的其他内容的持续时间。

      对于VOD，范围始终以零开头，并且结束值等于在流（广告）中插入的主内容持续时间和其他内容的持续时间的总和。

      对于线性／实时资产，该范围表示播放窗口范围，且该范围在播放期间会发生更改。

      TVSDK将调度一 `MediaPlayerItemEvent.ITEM_UPDATED` 个事件，以指示媒体项目已刷新，并且其属性（包括播放范围）已更新。

1. 使用Flex SDK中 `MediaPlayer` 公开 `HSlider` 的类和类上可用的方法设置搜索栏参数。

1. 使用计时器定期检索当前时间并更新 `SeekBar`。
