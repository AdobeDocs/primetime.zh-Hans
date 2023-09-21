---
description: 您可以将当前播放位置保存在视频中，并在未来会话中恢复在同一位置播放。
title: 保存视频位置并在稍后恢复
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# 保存视频位置并在稍后恢复{#save-the-video-position-and-resume-later}

您可以将当前播放位置保存在视频中，并在未来会话中恢复在同一位置播放。

动态插入的广告在用户会话之间有所不同，因此保存位置 **替换为** 拼接广告是指将来会话中的不同位置。 TVSDK提供了在忽略拼接广告时检索播放位置的方法。

1. 当用户退出视频时，您的应用程序将检索并保存视频中的位置。

   >[!TIP]
   >
   >不包括广告持续时间。

   由于广告模式、频率上限等，每个会话中的广告时间可能会有所不同。 一个会话中视频的当前时间可能会与将来会话中的不同。 在视频中保存位置时，应用程序检索本地时间。 使用 `localTime` 属性来读取此位置，您可以将该位置保存在设备上或服务器上的数据库中。

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   例如，如果用户位于视频的第20分钟，并且此位置包含五分钟的广告， `currentTime` 将 `be` 1200秒，而 `localTime` 此职位将 `be` 900秒。

1. 在播放器活动恢复时恢复用户会话。

   TVSDK不会在TVSDK初始化之间继续播放，因为它不会将任何信息保存在本地。 您的应用程序必须实施此逻辑。

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. 要在相同位置恢复视频，请执行以下操作：

   * 要从上一个会话中保存的位置恢复播放视频，请使用 `seekToLocal`.

     >[!TIP]
     >
     >仅使用本地时间值调用此方法。 如果使用当前时间结果调用方法，则会发生错误行为。

   * 要搜索到当前时间，请使用 `seek`.

1. 当您的应用程序收到 `onStatusChanged` 状态更改事件，搜索到保存的本地时间。
1. 提供在广告策略界面中指定的广告时间。
1. 通过扩展默认的广告策略选择器，实施自定义广告策略选择器。
1. 通过以下方式提供必须呈现给用户的广告时间： `selectAdBreaksToPlay`.

   当播放器进入已准备状态时，所有广告都已解析，因此 `AdPolicyInfo.adBreakTimelineItem` 属性包含本地时间位置之前的所有广告时间。 您的应用程序可以决定播放前置广告时间并继续到指定的本地时间，播放中置广告时间并继续到指定的本地时间，或不播放广告时间。
