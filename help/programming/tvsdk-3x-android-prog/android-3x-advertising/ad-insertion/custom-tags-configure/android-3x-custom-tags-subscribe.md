---
description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
seo-description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
seo-title: 订阅自定义标记
title: 订阅自定义标记
uuid: f1a934bd-772e-435f-84b5-cb48db23c06e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 订阅自定义标记 {#subscribe-to-custom-tags}

每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。

在播放开始之前，您必须订阅标记。 要获得有关HLS清单中自定义标记的通知，请执行以下操作：

1. 通过将包含自定义标记的数组传递给中，全局设置自定义广告标记 `setSubscribedTags` 名称 `MediaPlayerItemConfig`。

   >[!IMPORTANT]
   >
   >处理HLS流时 `#` 必须包含前缀。

   例如：

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```
