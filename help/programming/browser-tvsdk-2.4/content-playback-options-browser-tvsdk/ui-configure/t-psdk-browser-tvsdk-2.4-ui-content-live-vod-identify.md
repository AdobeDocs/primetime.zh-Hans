---
description: 您可能需要知道媒体内容是实时还是VOD。
title: 确定内容是实时内容还是VOD内容
exl-id: fb15c779-db25-4858-b7d7-ae5eabf646a3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# 确定内容是实时内容还是VOD内容{#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒体内容是实时还是VOD。

1. 等待浏览器TVSDK触发 `AdobePSDK.PSDKEventType.STATUS_CHANGED` 具有的事件 `event.status` 之 `AdobePSDK.MediaPlayerStatus.PREPARED`.

   此步骤可确保成功加载媒体资源。

   >[!IMPORTANT]
   >
   >如果浏览器TVSDK至少不在 `PREPARED` state，尝试调用以下方法会引发 `IllegalStateException`.

1. 读取 `live` 从 `MediaPlayerItem` 界面：

   ```js
   player.currentItem.live
   ```
