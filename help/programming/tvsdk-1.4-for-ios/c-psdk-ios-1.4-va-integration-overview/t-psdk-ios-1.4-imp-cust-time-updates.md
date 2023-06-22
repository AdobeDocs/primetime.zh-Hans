---
description: 在某些Analytics实施中，客户端应用程序可能希望提供一个与TVSDK的localTime值所报告的位置不同的播放头位置。 例如，在线性流播放期间，每个节目的播放头可相对于其开始时间提供。
title: 实施自定义时间更新
exl-id: 85ec4744-541f-451f-95a3-063dd1151635
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 实施自定义时间更新{#implement-custom-time-updates}

在某些Analytics实施中，客户端应用程序可能希望提供一个与TVSDK的localTime值所报告的位置不同的播放头位置。 例如，在线性流播放期间，每个节目的播放头可相对于其开始时间提供。

>[!TIP]
>
>仅当要提供的播放头位置与默认位置不同时，才覆盖此方法。

1. 覆盖默认播放头位置：

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >在此代码示例中，500只是一个示例值。 您需要为自定义播放头位置使用其他值。
