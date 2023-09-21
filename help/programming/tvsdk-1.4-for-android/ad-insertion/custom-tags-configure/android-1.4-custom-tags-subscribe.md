---
description: 每次在内容清单中遇到订阅的标记时，TVSDK都会为这些对象准备TimedMetadata。
title: 订阅自定义标记
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 订阅自定义标记{#subscribe-to-custom-tags}

每次在内容清单中遇到订阅的标记时，TVSDK都会为这些对象准备TimedMetadata。

在开始播放之前，必须订阅标记。
要接收有关HLS清单中自定义标记的通知，请执行以下操作：

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
