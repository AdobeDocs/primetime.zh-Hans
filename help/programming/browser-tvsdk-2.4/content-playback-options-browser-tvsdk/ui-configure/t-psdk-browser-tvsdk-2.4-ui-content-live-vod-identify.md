---
description: 您可能需要知道媒体内容是实时还是VOD。
seo-description: 您可能需要知道媒体内容是实时还是VOD。
seo-title: 确定内容是实时还是VOD
title: 确定内容是实时还是VOD
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# 确定内容是实时还是VOD{#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒体内容是实时还是VOD。

1. 等待浏览器TVSDK触发`AdobePSDK.PSDKEventType.STATUS_CHANGED`事件,`event.status`为`AdobePSDK.MediaPlayerStatus.PREPARED`。

   此步骤可确保媒体资源已成功加载。

   >[!IMPORTANT]
   >
   >如果浏览器TVSDK至少不处于`PREPARED`状态，则尝试调用以下方法将引发`IllegalStateException`。

1. 从`MediaPlayerItem`接口读取`live`:

   ```js
   player.currentItem.live
   ```

