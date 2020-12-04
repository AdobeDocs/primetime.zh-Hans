---
description: 在某些情况下，您需要了解媒体内容是实时还是VOD。
seo-description: 在某些情况下，您需要了解媒体内容是实时还是VOD。
seo-title: 确定内容是实时还是VOD
title: 确定内容是实时还是VOD
uuid: cd71b8d3-259a-48f8-a6ad-02b57da146a7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 确定内容是实时还是VOD{#identify-whether-the-content-is-live-or-vod}

在某些情况下，您需要了解媒体内容是实时还是VOD。

1. 确保播放器至少处于PREPARED状态。
1. 确定`MediaPlayerItem`内容是实时(true)还是VOD(false)。

   ```java
   boolean isLive();
   ```

