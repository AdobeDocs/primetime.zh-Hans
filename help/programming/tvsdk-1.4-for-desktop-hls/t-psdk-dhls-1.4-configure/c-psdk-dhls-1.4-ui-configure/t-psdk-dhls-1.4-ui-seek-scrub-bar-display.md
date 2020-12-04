---
description: TVSDK支持在视频点播(VOD)和直播流中搜索流是滑动窗口播放列表的特定位置（时间）。
seo-description: TVSDK支持在视频点播(VOD)和直播流中搜索流是滑动窗口播放列表的特定位置（时间）。
seo-title: 显示具有当前播放位置的搜索滑动条
title: 显示具有当前播放位置的搜索滑动条
uuid: f940b305-4893-4531-9a79-53670f5fd23f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# 显示具有当前播放位置{#display-a-seek-scrub-bar-with-the-current-playback-position}的搜索滑动条

TVSDK支持在视频点播(VOD)和直播流中搜索流是滑动窗口播放列表的特定位置（时间）。

>[!IMPORTANT]
>
>在实时流中搜索仅允许DVR。

1. 设置搜索回呼。

       搜索是异步的，因此TVSDK将分派以下搜索相关事件:
   
   * `SeekEvent.SEEK_BEGIN` -开始寻找。
   * `SeekEvent.SEEK_END` -寻求成功。
   * `SeekEvent.SEEK_POSITION_ADJUSTED` -重新调整用户提供的搜索位置。

1. 等待播放器处于有效状态进行搜索。

   有效状态包括PREPARED、COMPLETED、PAUSED和PLAYING。

1. 侦听适当的事件，以查看用户正在擦洗的时间。
1. 将请求的搜索位置（毫秒）传递给`MediaPlayer.seek`方法。

   ```
   function seek(position:Number):void;
   ```

   您只能在资产的可搜索持续时间内进行搜索。 对于视频点播，持续时间从0到资产的持续时间。

   >[!TIP]
   >
   >这会将播放头移动到流中的新位置，但最终计算位置可能与指定的搜索位置不同。

1. 等待TVSDK分派`SeekEvent.SEEK_END`事件。
1. 使用事件.actualPosition检索最终调整的播放位置。

       这很重要，因为搜索后的实际开始位置可能与请求的位置不同。可能会应用各种规则，包括：
   
   * 如果搜索或其他重新定位在广告中断的中间结束或跳过广告中断，则播放行为会受到影响。
   * 如果在段边界附近进行搜索，则搜索位置将调整为段的开头。

1. 在显示搜索拖拽栏时使用位置信息。
