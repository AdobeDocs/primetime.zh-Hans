---
description: 您可以在视频中保存当前播放位置，并在将来的会话中在相同位置继续播放。
title: 保存视频位置并稍后恢复
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---


# 保存视频位置并稍后恢复{#save-the-video-position-and-resume-later}

您可以在视频中保存当前播放位置，并在将来的会话中在相同位置继续播放。

动态插入的广告在用户会话之间有所不同，因此将位置&#x200B;**与**&#x200B;拼接的广告保存后，将在将来会话中的位置不同。 TVSDK提供方法来检索播放位置，同时忽略拼接的广告。

1. 当用户退出视频时，您的应用程序将检索并保存视频中的位置。

   >[!TIP]
   >
   >不包括广告期。

   由于广告模式、频率限制等原因，每个会话中的广告中断可能会有所不同。 在将来的会话中，视频在一个会话中的当前时间可能有所不同。 在视频中保存位置时，应用程序会检索本地时间。 使用`localTime`属性读取此位置，可将该位置保存在设备上或服务器上的数据库中。

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   例如，如果用户在视频的第20分钟，且此位置包含5分钟广告，则`currentTime`将`be` 1200秒，而此位置的`localTime`将`be` 900秒。

1. 在播放器活动恢复时恢复用户会话。

   TVSDK不会在TVSDK初始化之间恢复播放，因为它不会在本地保存任何信息。 您的应用程序必须实现此逻辑。

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. 要在同一位置恢复视频，请执行以下操作：

   * 要从从上一会话中保存的位置继续播放视频，请使用`seekToLocal`。

      >[!TIP]
      >
      >只使用本地时间值调用此方法。 如果使用当前时间结果调用该方法，则会发生错误行为。

   * 要查找当前时间，请使用`seek`。

1. 当应用程序收到`onStatusChanged`状态更改事件时，请查找保存的本地时间。
1. 按照广告策略接口中的指定提供广告中断。
1. 通过扩展默认广告策略选择器来实施自定义广告策略选择器。
1. 通过实施`selectAdBreaksToPlay`提供必须向用户显示的广告分段。

   当播放器进入PREPARED状态时，所有广告都已解析，因此`AdPolicyInfo.adBreakTimelineItem`属性包含本地时间位置之前的所有广告中断。 您的应用程序可以决定播放前置广告中断，并恢复到指定的本地时间，播放中间广告中断，恢复到指定的本地时间，或者不播放广告中断。
