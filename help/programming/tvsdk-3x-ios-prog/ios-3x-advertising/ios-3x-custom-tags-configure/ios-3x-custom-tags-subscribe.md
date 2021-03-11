---
description: 每次在内容清单中遇到订阅标记时，TVSDK会为这些对象准备PTTimedMetadata对象。
title: 订阅自定义标记
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# 订阅自定义标记{#subscribe-to-custom-tags}

每次在内容清单中遇到订阅标记时，TVSDK会为这些对象准备PTTimedMetadata对象。

在播放开始之前，您必须订阅这些标记。
要通知有关HLS清单中的自定义标记：

1. 通过将包含自定义标记的数组传递到`PTSDKConfig`中的`setSubscribedTags`，全局设置自定义广告标记名称。

   >[!IMPORTANT]
   >
   >处理HLS流时必须包含`#`前缀。

   例如：

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
