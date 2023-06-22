---
description: 在某些情况下，您需要知道媒体内容是实时内容还是VOD。
title: 确定内容是实时内容还是VOD内容
exl-id: b93cc61b-aa72-4edd-a070-93c111dec339
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# 确定内容是实时内容还是VOD内容{#identify-whether-the-content-is-live-or-vod}

在某些情况下，您需要知道媒体内容是实时内容还是VOD。

1. 确保播放器至少处于“已准备”状态。
1. 确定 `MediaPlayerItem` 内容为实时(true)或VOD(false)。

   ```java
   boolean isLive();
   ```
