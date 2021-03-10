---
description: TVSDK支持搜索到某个特定位置（时间），在该位置，流是视频点播(VOD)和直播流中的滑动窗口播放列表。
title: 使用当前播放位置显示搜索拖拉栏
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# 显示当前播放位置{#display-a-seek-scrub-bar-with-the-current-playback-position}的搜索滑动条

TVSDK支持搜索到某个特定位置（时间），在该位置，流是视频点播(VOD)和直播流中的滑动窗口播放列表。

>[!IMPORTANT]
>
>仅DVR允许在实时流中搜索。

1. 设置搜索回呼。

       搜索是异步的，因此TVSDK调度以下与搜索相关的事件:
   
   * `SeekEvent.SEEK_BEGIN`  — 开始搜寻。
   * `SeekEvent.SEEK_END`  — 寻求成功。
   * `SeekEvent.SEEK_POSITION_ADJUSTED`  — 重新调整了用户提供的搜索位置。

1. 等待播放器处于有效状态进行搜索。

   有效状态包括PREPARED、COMPLETED、PAUSED和PLAYING。

1. 侦听相应的事件，以查看用户正在擦洗的时间。
1. 将请求的搜索位置（毫秒）传递给`MediaPlayer.seek`方法。

   ```
   function seek(position:Number):void;
   ```

   您只能在资产的可搜索持续时间中进行搜索。 对于视频点播，持续时间从0到资产的持续时间。

   >[!TIP]
   >
   >这会将播放头移动到流中的新位置，但最终计算的位置可能与指定的搜索位置不同。

1. 等待TVSDK调度`SeekEvent.SEEK_END`事件。
1. 使用事件.actualPosition检索最终调整的播放位置。

       这很重要，因为搜索后的实际开始位置可能与请求的位置不同。可能适用各种规则，包括：
   
   * 如果搜索或其他重新定位在广告中断或跳过广告中断的中间结束，则播放行为会受到影响。
   * 如果在段边界附近搜索，则搜索位置将调整为段的开头。

1. 显示搜索拖拽栏时使用位置信息。
