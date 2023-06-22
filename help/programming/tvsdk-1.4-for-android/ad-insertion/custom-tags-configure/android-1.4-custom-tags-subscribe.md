---
description: 每次在内容清单中遇到订阅标记的对象时，TVSDK都会为这些对象准备TimedMetadata对象。
title: 订阅自定义标记
exl-id: 7f1f86ca-eeba-43c3-ac2a-c493d05ad73a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 订阅自定义标记{#subscribe-to-custom-tags}

每次在内容清单中遇到订阅标记的对象时，TVSDK都会为这些对象准备TimedMetadata对象。

在开始播放之前，您必须订阅标记。
要接收有关HLS清单中的自定义标记的通知，请执行以下操作：

通过将包含自定义标记的数组传递到，全局设置自定义广告标记名称 `setSubscribedTags` 在 `MediaPlayerItemConfig`.

>[!IMPORTANT]
>
>您必须包含 `#` 使用HLS流时的前缀。

例如：

```java
String[] array = new String[3]; 
array[0] = "#EXT-X-ASSET"; 
array[1] = "#EXT-X-BLACKOUT"; 
array[2] = "#EXT-OATCLS-SCTE35"; 
MediaPlayerItemConfig.setSubscribedTags(array);
```
