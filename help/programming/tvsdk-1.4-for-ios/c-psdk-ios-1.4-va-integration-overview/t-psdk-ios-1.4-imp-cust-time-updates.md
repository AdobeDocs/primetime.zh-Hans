---
description: 在一些Analytics实施中，客户端应用程序可能希望提供一个与TVSDK的localTime值所报告的位置不同的播放头位置。 例如，在线性流播放期间，每个节目的播放头可相对于其开始时间提供。
title: 实施自定义时间更新
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 实施自定义时间更新{#implement-custom-time-updates}

在一些Analytics实施中，客户端应用程序可能希望提供一个与TVSDK的localTime值所报告的位置不同的播放头位置。 例如，在线性流播放期间，每个节目的播放头可相对于其开始时间提供。

>[!TIP]
>
>仅当要提供的播放头位置不同于默认位置时，才覆盖此方法。

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
