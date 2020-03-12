---
description: 您可能需要了解媒体内容是实时的还是VOD的。
seo-description: 您可能需要了解媒体内容是实时的还是VOD的。
seo-title: 确定内容是实时的还是VOD的
title: 确定内容是实时的还是VOD的
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 确定内容是实时的还是VOD的{#identify-whether-the-content-is-live-or-vod}

您可能需要了解媒体内容是实时的还是VOD的。

1. 等待浏览器TVSDK触发 `AdobePSDK.PSDKEventType.STATUS_CHANGED` 事件( `event.status` 共 `AdobePSDK.MediaPlayerStatus.PREPARED`)。

   此步骤可确保媒体资源已成功加载。

   >[!IMPORTANT]
   >
   >如果Browser TVSDK至少未处于状态， `PREPARED` 则尝试调用以下方法将引发错误 `IllegalStateException`。

1. 从界 `live` 面读 `MediaPlayerItem` 取：

   ```js
   player.currentItem.live
   ```

