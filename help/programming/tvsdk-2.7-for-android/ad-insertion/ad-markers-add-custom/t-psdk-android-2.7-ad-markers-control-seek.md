---
description: 在使用自定义广告标记时，您可以覆盖TVSDK处理如何搜索广告的默认行为。
title: 控制通过自定义广告标记进行搜索的播放行为
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 控制搜索自定义广告标记{#control-playback-behavior-for-seeking-over-custom-ad-markers}的播放行为

在使用自定义广告标记时，您可以覆盖TVSDK处理如何搜索广告的默认行为。

默认情况下，当用户在放置自定义广告标记后搜索或查看过去的广告部分时，TVSDK会跳过广告。 这可能与标准广告中断的当前播放行为不同。 您可以设置TVSDK将播放头重新定位到用户搜索超过一个或多个自定义广告时最近跳过的自定义广告的开头。

1. 用`true`调用`CustomRangeMetadata.setAdjustSeekPosition`。

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

