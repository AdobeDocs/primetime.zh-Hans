---
description: 每次在内容清单中遇到订阅标记的对象时，TVSDK都会为这些对象准备PTTimedMetadata对象。
title: 订阅自定义标记
exl-id: 5074e622-8824-4253-a668-485e2f68f156
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 订阅自定义标记 {#subscribe-to-custom-tags}

每次在内容清单中遇到订阅标记的对象时，TVSDK都会为这些对象准备PTTimedMetadata对象。

在开始播放之前，您必须订阅标记。
要接收有关HLS清单中的自定义标记的通知，请执行以下操作：

1. 通过将包含自定义标记的数组传递到，全局设置自定义广告标记名称 `setSubscribedTags` 在 `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >您必须包含 `#` 使用HLS流时的前缀。

   例如：

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
