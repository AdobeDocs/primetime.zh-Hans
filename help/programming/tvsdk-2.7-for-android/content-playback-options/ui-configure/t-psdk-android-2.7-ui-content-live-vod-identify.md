---
description: 您可能需要了解媒体内容是实时的还是视频点播(VOD)。
seo-description: 您可能需要了解媒体内容是实时的还是视频点播(VOD)。
seo-title: 确定内容是实时的还是VOD的
title: 确定内容是实时的还是VOD的
uuid: d49315ee-8cec-4b79-adbd-a49c2a527424
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 确定内容是实时的还是VOD的 {#identify-whether-the-content-is-live-or-vod}

您可能需要了解媒体内容是实时的还是视频点播(VOD)。

1. 确保播放器至少处于状 `PREPARED` 态。
1. 确定内 `MediaPlayerItem` 容是实时( `true`)还是VOD( `false`)。

   ```java
   boolean isLive();
   ```
