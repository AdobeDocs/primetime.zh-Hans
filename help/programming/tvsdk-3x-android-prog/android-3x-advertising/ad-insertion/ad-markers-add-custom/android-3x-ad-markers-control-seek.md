---
description: 您可以在使用自定义广告标记时覆盖TVSDK处理如何搜索广告的默认行为。
seo-description: 您可以在使用自定义广告标记时覆盖TVSDK处理如何搜索广告的默认行为。
seo-title: 控制用于搜索自定义广告标记的播放行为
title: 控制用于搜索自定义广告标记的播放行为
uuid: ec95a22f-0143-4c80-826f-d6b40e77cf26
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 控制用于搜索自定义广告标记的播放行为 {#control-playback-behavior-for-seeking-over-custom-ad-markers}

您可以在使用自定义广告标记时覆盖TVSDK处理如何搜索广告的默认行为。

默认情况下，当用户搜索自定义广告标记所产生的广告部分或以前的广告部分时，TVSDK会跳过广告。 这可能与标准广告中断的当前播放行为不同。 您可以设置TVSDK将播放头重新定位到用户搜索超过一个或多个自定义广告时最近跳过的自定义广告的开头。

1. 请致 `CustomRangeMetadata.setAdjustSeekPosition` 电 `true`。

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. 使用 `customRangeMetadata` 于 `MediaPlayerItemConfig`。

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
