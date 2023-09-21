---
description: 您可能需要了解媒体内容是实时的还是视频点播(VOD)。
title: 识别内容是实时内容还是VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# 识别内容是实时内容还是VOD {#identify-whether-the-content-is-live-or-vod}

您可能需要了解媒体内容是实时的还是视频点播(VOD)。

1. 确保播放器至少处于 `PREPARED` 省/州。
1. 确定 `MediaPlayerItem` 内容已上线( `true`)或VOD ( `false`)。

   ```java
   boolean isLive();
   ```
