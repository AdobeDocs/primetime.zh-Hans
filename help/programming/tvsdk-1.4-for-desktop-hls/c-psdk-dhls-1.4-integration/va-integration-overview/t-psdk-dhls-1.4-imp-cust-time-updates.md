---
description: 在某些Analytics实施中，客户端应用程序可能希望提供一个与TVSDK localTime值报告的播放头位置不同的播放头位置。 例如，在LINEAR流播放期间，每个节目的播放头可以相对于其开始时间提供。
title: 实施自定义时间更新
exl-id: be0f2684-6a17-4d99-8875-7f404ce8a656
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 实施自定义时间更新{#implement-custom-time-updates}

在某些Analytics实施中，客户端应用程序可能希望提供一个与TVSDK localTime值报告的播放头位置不同的播放头位置。 例如，在LINEAR流播放期间，每个节目的播放头可以相对于其开始时间提供。

>[!TIP]
>
>仅当您想提供不同于默认位置的播放头位置时，才覆盖此方法。

1. 覆盖默认播放头位置：

   ```
   vaMetadata.currentTimeUpdateBlock = function():Number { 
      if (currentTime == 0) { 
          currentTime = getTimer(); 
      } 
      return ((getTimer() - currentTime) / 1000 + 1000); 
   }
   ```

   >[!IMPORTANT]
   >
   >此代码片段中的值仅为示例。 您需要为自定义播放头位置使用不同的值。
