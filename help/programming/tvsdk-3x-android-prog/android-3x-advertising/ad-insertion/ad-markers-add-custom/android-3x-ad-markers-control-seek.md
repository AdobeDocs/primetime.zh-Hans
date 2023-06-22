---
description: 您可以使用自定义广告标记覆盖TVSDK处理如何在广告上搜寻的默认行为。
title: 控制对自定义广告标记进行搜寻的播放行为
exl-id: c148aca6-699d-4b93-9013-9e20bc391687
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 控制对自定义广告标记进行搜寻的播放行为 {#control-playback-behavior-for-seeking-over-custom-ad-markers}

您可以使用自定义广告标记覆盖TVSDK处理如何在广告上搜寻的默认行为。

默认情况下，当用户搜寻或浏览因放置自定义广告标记而生成的广告部分时，TVSDK会跳过广告。 这可能与标准广告时间的当前播放行为不同。 当用户搜寻超过一个或多个自定义广告时，您可以设置TVSDK将播放头重新定位到最近跳过的自定义广告的开头。

1. 调用 `CustomRangeMetadata.setAdjustSeekPosition` 替换为 `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. 使用 `customRangeMetadata` 在 `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
