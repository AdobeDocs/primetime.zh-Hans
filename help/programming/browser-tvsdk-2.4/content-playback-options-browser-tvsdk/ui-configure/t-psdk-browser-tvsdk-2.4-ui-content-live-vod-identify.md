---
description: 您可能需要知道媒体内容是实时还是VOD。
title: 识别内容是实时内容还是VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# 识别内容是实时内容还是VOD{#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒体内容是实时还是VOD。

1. 等待浏览器TVSDK触发 `AdobePSDK.PSDKEventType.STATUS_CHANGED` 事件包含 `event.status` 之 `AdobePSDK.MediaPlayerStatus.PREPARED`.

   此步骤可确保成功加载媒体资源。

   >[!IMPORTANT]
   >
   >如果浏览器TVSDK至少不在 `PREPARED` 状态，尝试调用以下方法会引发 `IllegalStateException`.

1. 读取 `live` 从 `MediaPlayerItem` 界面：

   ```js
   player.currentItem.live
   ```
