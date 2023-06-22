---
description: 您可能需要了解媒体内容是实时还是视频点播(VOD)。
title: 确定内容是实时内容还是VOD内容
exl-id: 756d4f04-d354-4194-80c9-c2ea6198a566
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# 确定内容是实时内容还是VOD内容 {#identify-whether-the-content-is-live-or-vod}

您可能需要了解媒体内容是实时还是视频点播(VOD)。

1. 确保播放器至少处于 `PREPARED` 省/州。
1. 确定 `MediaPlayerItem` 内容已上线( `true`)或VOD ( `false`)。

   ```java
   boolean isLive();
   ```
