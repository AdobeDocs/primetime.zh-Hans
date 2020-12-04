---
description: 在使用自定义广告标记时，您可以覆盖TVSDK处理如何搜索广告的默认行为。
seo-description: 在使用自定义广告标记时，您可以覆盖TVSDK处理如何搜索广告的默认行为。
seo-title: 控制用于搜索自定义广告标记的播放行为
title: 控制用于搜索自定义广告标记的播放行为
uuid: 248e914e-81b7-4aa5-a4d5-06ca2666e006
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# 控制搜索自定义广告标记{#control-playback-behavior-for-seeking-over-custom-ad-markers}的播放行为

在使用自定义广告标记时，您可以覆盖TVSDK处理如何搜索广告的默认行为。

默认情况下，当用户搜索或通过放置自定义广告标记所产生的广告部分时，TVSDK会跳过广告。 这可能与标准广告中断的当前播放行为不同。 您可以设置TVSDK，当用户搜索超过一个或多个自定义广告时，将播放头重新定位到最近跳过的自定义广告的开头。

1. 使用`true`调用`CustomRangeMetadata.setAdjustSeekPosition`。

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. 在`MediaPlayerItemConfig`中使用`customRangeMetadata`。

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```

