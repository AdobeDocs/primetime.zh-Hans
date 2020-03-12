---
description: 您可能需要了解媒体内容是实时的还是视频点播(VOD)。
seo-description: 您可能需要了解媒体内容是实时的还是视频点播(VOD)。
seo-title: 确定内容是实时的还是VOD的
title: 确定内容是实时的还是VOD的
uuid: e6a66104-97fb-438a-8356-e21f94058c85
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 确定内容是实时的还是VOD的 {#identify-whether-the-content-is-live-or-vod}

您可能需要了解媒体内容是实时的还是视频点播(VOD)。

1. 确保播放器至少处于状 `PREPARED` 态。
1. 确定内 `MediaPlayerItem` 容是实时( `true`)还是VOD( `false`)。

   ```java
   boolean isLive();
   ```
