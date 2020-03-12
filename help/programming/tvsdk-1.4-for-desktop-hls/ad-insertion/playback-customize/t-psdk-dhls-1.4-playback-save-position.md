---
description: 您可以保存视频中的当前播放位置，并在将来的会话中在相同位置继续播放。
seo-description: 您可以保存视频中的当前播放位置，并在将来的会话中在相同位置继续播放。
seo-title: 保存视频位置，稍后恢复
title: 保存视频位置，稍后恢复
uuid: 03ed5c63-008d-4dd1-9a31-baefa73b56e2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 保存视频位置，稍后恢复{#save-the-video-position-and-resume-later}

您可以保存视频中的当前播放位置，并在将来的会话中在相同位置继续播放。

动态插入的广告在用户会话之间有所不同，因此用拼接的 **广告保存位置** ，是指将来会话中的不同位置。 TVSDK提供了在忽略拼接广告时检索播放位置的方法。

1. 当用户退出视频时，应用程序将检索并保存视频中的位置。

   >[!TIP]
   >
   >不包括广告持续时间。

   由于广告模式、频率限制等原因，每个会话中的广告中断可能会有所不同。 在将来的会话中，视频在一个会话中的当前时间可能不同。 在视频中保存位置时，应用程序会检索本地时间。 使用属 `localTime` 性读取此位置，该位置可保存在设备上或服务器上的数据库中。

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   例如，如果用户在视频的第20分钟，并且此位置包括5分钟的广告，则为 `currentTime` 1200秒，而 `be` 此位置为 `localTime``be` 900秒。

1. 恢复播放器活动时恢复用户会话。

   TVSDK不会在TVSDK初始化之间恢复播放，因为它不会在本地保存任何信息。 您的应用程序必须实现此逻辑。

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. 要在同一位置恢复视频，请执行以下操作：

   * 要从从上一会话保存的位置继续播放视频，请使用 `seekToLocal`。

      >[!TIP]
      >
      >仅使用本地时间值调用此方法。 如果使用当前时间结果调用该方法，则会发生错误行为。

   * 要寻找当前时间，请使用 `seek`。

1. 当应用程序收到状 `onStatusChanged` 态更改事件时，请搜索保存的本地时间。
1. 按照广告策略界面中的指定提供广告中断。
1. 通过扩展默认广告策略选择器来实施自定义广告策略选择器。
1. 提供必须通过实施向用户展示的广告中断 `selectAdBreaksToPlay`。

   当播放器进入PREPARED状态时，所有广告都已解析，因此该属性包含 `AdPolicyInfo.adBreakTimelineItem` 本地时间位置之前的所有广告分段。 您的应用程序可以决定播放前置广告中断并恢复到指定的本地时间，播放中间广告中断并恢复到指定的本地时间，或者不播放广告中断。
