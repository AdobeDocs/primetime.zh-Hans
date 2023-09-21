---
description: 您可以使用TVSDK检索可在搜寻栏上显示的媒体信息。
title: 显示视频的持续时间、当前时间和剩余时间
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 显示视频的持续时间、当前时间和剩余时间{#display-the-duration-current-time-and-remaining-time-of-the-video}

您可以使用TVSDK检索可在搜寻栏上显示的媒体信息。

1. 等待播放器处于INITIALIZED状态。
1. 使用检索当前播放头时间 `MediaPlayer.currentTime` 属性。

   这将返回虚拟时间轴上的当前播放头位置（以毫秒为单位）。 所计算的时间相对于解析流而言可能包含替代内容的多个实例，例如连接到主流的多个广告或广告时间。 对于实时/线性流，返回的时间始终在播放窗口范围内。

   ```
   function get currentTime():Number;
   ```

1. 检索流的播放范围并确定持续时间。
   1. 使用 `mediaPlayer.playbackRange` 属性以获取虚拟时间线时间范围。

      ```
      function get playbackRange():TimeRange;
      ```

   1. 使用以下方式解析时间范围 `mediacore.utils.TimeRange`.
   1. 要确定持续时间，请从范围的末尾减去开始时间。

      这包括插入到流（广告）中的附加内容的持续时间。

      对于VOD，范围始终从零开始，并且结束值等于主内容持续时间与插入到流（广告）中的其他内容的持续时间之和。

      对于线性/实时资源，范围表示播放窗口范围，此范围在播放期间会更改。

      TVSDK调度 `MediaPlayerItemEvent.ITEM_UPDATED` 指示媒体项目已刷新并且其属性（包括播放范围）已更新的事件。

1. 使用上的可用方法 `MediaPlayer` 和 `HSlider` 在Flex SDK中公开可用以设置搜寻栏参数的类。

1. 使用计时器定期检索当前时间并更新 `SeekBar`.
