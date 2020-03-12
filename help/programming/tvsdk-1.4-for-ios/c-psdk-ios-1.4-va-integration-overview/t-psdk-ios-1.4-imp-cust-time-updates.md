---
description: 在某些分析实施中，客户端应用程序可能希望提供与TVSDK的localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于每个节目的开始时间提供每个节目的播放头。
seo-description: 在某些分析实施中，客户端应用程序可能希望提供与TVSDK的localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于每个节目的开始时间提供每个节目的播放头。
seo-title: 实施自定义时间更新
title: 实施自定义时间更新
uuid: 303303eb-c371-4766-a1ee-806ba75b4e01
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 实施自定义时间更新{#implement-custom-time-updates}

在某些分析实施中，客户端应用程序可能希望提供与TVSDK的localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于每个节目的开始时间提供每个节目的播放头。

>[!TIP]
>
>仅当要提供不同于默认位置的播放头位置时，才覆盖此方法。

1. 要覆盖默认播放头位置，请执行以下操作：

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >在此代码示例中，500只是示例值。 您需要为自定义播放头位置使用不同的值。

