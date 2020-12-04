---
description: 您可能需要知道媒体内容是实时内容还是视频点播(VOD)。
seo-description: 您可能需要知道媒体内容是实时内容还是视频点播(VOD)。
seo-title: 确定内容是实时还是VOD
title: 确定内容是实时还是VOD
uuid: d49315ee-8cec-4b79-adbd-a49c2a527424
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 确定内容是实时还是VOD {#identify-whether-the-content-is-live-or-vod}

您可能需要知道媒体内容是实时内容还是视频点播(VOD)。

1. 确保播放器至少处于`PREPARED`状态。
1. 确定`MediaPlayerItem`内容是实时(`true`)还是VOD(`false`)。

   ```java
   boolean isLive();
   ```
