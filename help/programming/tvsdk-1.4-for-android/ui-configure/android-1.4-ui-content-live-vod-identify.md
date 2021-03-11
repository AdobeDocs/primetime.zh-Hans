---
description: 在某些情况下，您需要了解媒体内容是实时的还是VOD的。
title: 确定内容是实时的还是VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# 确定内容是实时的还是VOD{#identify-whether-the-content-is-live-or-vod}

在某些情况下，您需要了解媒体内容是实时的还是VOD的。

1. 确保播放器至少处于PREPARED状态。
1. 确定`MediaPlayerItem`内容是实时(true)还是VOD(false)。

   ```java
   boolean isLive();
   ```

