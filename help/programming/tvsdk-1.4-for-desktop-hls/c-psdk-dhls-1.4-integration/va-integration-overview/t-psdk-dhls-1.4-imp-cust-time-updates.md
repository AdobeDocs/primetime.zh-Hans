---
description: 在某些分析实施中，客户端应用程序可能希望提供与TVSDK localTime值所报告的播放头位置不同的播放头位置。 例如，在LINEAR流播放期间，可以相对于每个项目的开始时间提供其播放头。
title: 实施自定义时间更新
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# 实现自定义时间更新{#implement-custom-time-updates}

在某些分析实施中，客户端应用程序可能希望提供与TVSDK localTime值所报告的播放头位置不同的播放头位置。 例如，在LINEAR流播放期间，可以相对于每个项目的开始时间提供其播放头。

>[!TIP]
>
>仅当要提供与默认位置不同的播放头位置时，才覆盖此方法。

1. 要覆盖默认播放指示器位置，请执行以下操作：

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
   >此代码片断中的值只是示例。 您需要对自定义播放头位置使用不同的值。

