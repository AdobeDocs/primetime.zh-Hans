---
description: 在某些情况下，您需要知道媒体内容是实时还是VOD。
title: 识别内容是实时内容还是VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 识别内容是实时内容还是VOD{#identify-whether-the-content-is-live-or-vod}

在某些情况下，您需要知道媒体内容是实时还是VOD。

1. 确保播放器至少处于“已准备”状态。
1. 确定 `MediaPlayerItem` 内容为实时(true)或VOD(false)。

   ```java
   boolean isLive();
   ```
