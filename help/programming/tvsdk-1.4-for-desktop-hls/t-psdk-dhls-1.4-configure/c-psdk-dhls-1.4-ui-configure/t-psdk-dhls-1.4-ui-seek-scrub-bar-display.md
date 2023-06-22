---
description: TVSDK支持在视频点播(VOD)和实时流中搜索流是滑动窗口播放列表的特定位置（时间）。
title: 显示具有当前播放位置的搜寻清理栏
exl-id: a85a06d8-040e-435a-8f55-9df5af3babe1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 显示具有当前播放位置的搜寻清理栏{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK支持在视频点播(VOD)和实时流中搜索流是滑动窗口播放列表的特定位置（时间）。

>[!IMPORTANT]
>
>只有DVR才允许在实时流中进行搜寻。

1. 设置用于搜寻的回调。

       搜索是异步执行的，因此TVSDK会调度以下与搜索相关的事件：
   
   * `SeekEvent.SEEK_BEGIN`  — 搜寻开始。
   * `SeekEvent.SEEK_END`  — 搜寻成功。
   * `SeekEvent.SEEK_POSITION_ADJUSTED`  — 重新调整了用户提供的搜寻位置。

1. 等待播放器处于有效的状态以进行搜寻。

   有效状态为“已准备”、“已完成”、“已暂停”和“正在播放”。

1. 侦听相应的事件，以查看用户何时进行清理。
1. 将请求的搜寻位置（毫秒）传递给 `MediaPlayer.seek` 方法。

   ```
   function seek(position:Number):void;
   ```

   您只能在资产的可搜索持续时间内查找。 对于点播视频，持续时间介于0到资源的持续时间之间。

   >[!TIP]
   >
   >这会将播放头移动到流中的新位置，但最终计算位置可能与指定的搜寻位置不同。

1. 等待TVSDK调度 `SeekEvent.SEEK_END` 事件。
1. 使用event.actualPosition检索最终调整的播放位置。

       这很重要，因为搜寻后的实际开始位置可能与请求位置不同。 可能适用各种规则，包括：
   
   * 如果搜寻或其他重新定位在广告时间中间终止或跳过广告时间，则播放行为会受到影响。
   * 如果在区段边界附近进行搜寻，则搜寻位置会调整到区段的开头。

1. 显示搜寻拖移栏时使用位置信息。
