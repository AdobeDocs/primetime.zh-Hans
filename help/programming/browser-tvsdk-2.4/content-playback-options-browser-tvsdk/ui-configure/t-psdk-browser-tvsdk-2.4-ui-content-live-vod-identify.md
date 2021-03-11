---
description: 您可能需要了解媒体内容是实时的还是VOD的。
title: 确定内容是实时的还是VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# 确定内容是实时的还是VOD{#identify-whether-the-content-is-live-or-vod}

您可能需要了解媒体内容是实时的还是VOD的。

1. 等待浏览器TVSDK触发`AdobePSDK.PSDKEventType.STATUS_CHANGED`事件,`event.status`为`AdobePSDK.MediaPlayerStatus.PREPARED`。

   此步骤可确保媒体资源已成功加载。

   >[!IMPORTANT]
   >
   >如果Browser TVSDK不至少处于`PREPARED`状态，则尝试调用以下方法将引发`IllegalStateException`。

1. 从`MediaPlayerItem`接口读取`live`:

   ```js
   player.currentItem.live
   ```

