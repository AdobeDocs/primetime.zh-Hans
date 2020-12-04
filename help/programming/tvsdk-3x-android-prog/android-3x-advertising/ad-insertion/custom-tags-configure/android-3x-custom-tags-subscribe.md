---
description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
seo-description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
seo-title: 订阅自定义标记
title: 订阅自定义标记
uuid: f1a934bd-772e-435f-84b5-cb48db23c06e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 1%

---


# 订阅自定义标记{#subscribe-to-custom-tags}

每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。

在播放开始之前，您必须订阅标记。 要通知有关HLS清单中的自定义标记：

1. 通过将包含自定义标记的数组传递到`MediaPlayerItemConfig`中的`setSubscribedTags`，全局设置自定义广告标记名称。

   >[!IMPORTANT]
   >
   >处理HLS流时必须包含`#`前缀。

   例如：

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```
