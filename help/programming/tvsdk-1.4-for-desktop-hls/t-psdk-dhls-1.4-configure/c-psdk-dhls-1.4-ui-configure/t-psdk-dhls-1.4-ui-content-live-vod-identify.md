---
description: 在某些情况下，您需要了解媒体内容是实时的还是VOD的。
seo-description: 在某些情况下，您需要了解媒体内容是实时的还是VOD的。
seo-title: 确定内容是实时的还是VOD的
title: 确定内容是实时的还是VOD的
uuid: 4d514c46-a1d0-4721-a423-92108126e37e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 确定内容是实时的还是VOD的{#identify-whether-the-content-is-live-or-vod}

在某些情况下，您需要了解媒体内容是实时的还是VOD的。

1. 确保播放器至少处于“已初始化”状态。
1. 确定内 `MediaPlayerItem` 容是实时(true)还是VOD(false)。

   ```
   function get isLive():Boolean;
   ```

