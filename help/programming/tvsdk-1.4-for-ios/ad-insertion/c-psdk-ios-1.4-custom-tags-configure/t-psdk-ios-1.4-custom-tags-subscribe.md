---
description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备PTTimedMetadata对象。
seo-description: 每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备PTTimedMetadata对象。
seo-title: 订阅自定义标记
title: 订阅自定义标记
uuid: de66d3db-46d1-485f-9d3a-6e28495bfb13
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 订阅自定义标记 {#subscribe-to-custom-tags}

每次在内容清单中遇到订阅标记时，TVSDK都会为这些对象准备PTTimedMetadata对象。

在播放开始之前，您必须订阅标记。
要获得有关HLS清单中自定义标记的通知，请执行以下操作：

1. 通过将包含自定义标记的数组传递给中，全局设置自定义广告标记 `setSubscribedTags` 名称 `PTSDKConfig`。

   >[!IMPORTANT]
   >
   >处理HLS流时 `#` 必须包含前缀。

   例如：

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```

