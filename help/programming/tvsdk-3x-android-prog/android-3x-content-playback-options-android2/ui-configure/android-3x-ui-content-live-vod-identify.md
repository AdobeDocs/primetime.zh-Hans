---
description: 您可能需要知道媒体内容是实时内容还是视频点播(VOD)。
seo-description: 您可能需要知道媒体内容是实时内容还是视频点播(VOD)。
seo-title: 确定内容是实时还是VOD
title: 确定内容是实时还是VOD
uuid: e6a66104-97fb-438a-8356-e21f94058c85
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
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
