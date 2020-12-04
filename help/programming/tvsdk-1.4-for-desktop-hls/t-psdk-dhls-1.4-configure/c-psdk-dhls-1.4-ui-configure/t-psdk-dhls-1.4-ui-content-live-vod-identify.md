---
description: 在某些情况下，您需要了解媒体内容是实时还是VOD。
seo-description: 在某些情况下，您需要了解媒体内容是实时还是VOD。
seo-title: 确定内容是实时还是VOD
title: 确定内容是实时还是VOD
uuid: 4d514c46-a1d0-4721-a423-92108126e37e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 确定内容是实时还是VOD{#identify-whether-the-content-is-live-or-vod}

在某些情况下，您需要了解媒体内容是实时还是VOD。

1. 确保播放器至少处于INITIALIZED状态。
1. 确定`MediaPlayerItem`内容是实时(true)还是VOD(false)。

   ```
   function get isLive():Boolean;
   ```

