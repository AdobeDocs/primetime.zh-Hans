---
description: 您可以使用TVSDK检索可在搜索栏上显示的媒体的相关信息。
title: 显示视频的持续时间、当前时间和剩余时间
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 显示视频的持续时间、当前时间和剩余时间{#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK检索可在搜索栏上显示的媒体的相关信息。

1. 等待播放器处于“已初始化”状态。
1. 使用`MediaPlayer.currentTime`属性检索当前播放头时间。

   这将返回虚拟时间线上的当前播放头位置（以毫秒为单位）。 时间是相对于可能包含多个替代内容实例（如多个广告或拼接到主流中的广告中断）的已解析流计算的。 对于实时/线性流，返回的时间始终在播放窗口范围内。

   ```
   function get currentTime():Number;
   ```

1. 检索流的播放范围并确定持续时间。
   1. 使用`mediaPlayer.playbackRange`属性获取虚拟时间线时间范围。

      ```
      function get playbackRange():TimeRange;
      ```

   1. 使用`mediacore.utils.TimeRange`分析时间范围。
   1. 要确定持续时间，请从范围的末尾减去开始。

      这包括插入流（广告）的其他内容的持续时间。

      对于VOD，范围始终以零开头，且结束值等于在流（广告）中插入的主内容持续时间和附加内容的持续时间之和。

      对于线性/实时资产，该范围表示播放窗口范围，且该范围在播放期间会更改。

      TVSDK调度`MediaPlayerItemEvent.ITEM_UPDATED`事件以指示媒体项已刷新，其属性（包括播放范围）已更新。

1. 使用Flex SDK中公开的`MediaPlayer`和`HSlider`类上的可用方法设置搜索栏参数。

1. 使用计时器定期检索当前时间并更新`SeekBar`。
