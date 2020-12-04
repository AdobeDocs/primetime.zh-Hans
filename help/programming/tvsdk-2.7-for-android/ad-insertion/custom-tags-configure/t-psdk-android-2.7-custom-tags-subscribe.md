---
description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
seo-description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备TimedMetadata对象。
seo-title: 订阅自定义标记
title: 订阅自定义标记
uuid: 9f74b2b9-bbc9-433c-8226-2c2b68eddf7e
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
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

