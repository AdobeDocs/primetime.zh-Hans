---
description: 在某些Analytics实施中，客户端应用程序可能希望提供一个与TVSDK localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，每个节目的播放头可相对于其开始时间提供。
title: 实施自定义时间更新
exl-id: 91e778ca-cdab-4c50-96f8-3333d210fd4a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 实施自定义时间更新 {#implement-custom-time-updates}

在某些Analytics实施中，客户端应用程序可能希望提供一个与TVSDK localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，每个节目的播放头可相对于其开始时间提供。

>[!TIP]
>
>仅当要提供默认位置以外的播放头位置时，才覆盖此方法。

覆盖默认播放头位置：

```java
vaMetadata.setCurrentTimeUpdateBlock(new VideoAnalyticsMetadata.CurrentTimeUpdateBlock() { 
    @Override 
    public long call() { 
        long range = 500L; 
        Random r = new Random() 
        return (long)(r.nextDouble()*range); 
    } 
});
```

>[!IMPORTANT]
>
>此代码片段中的值仅为示例。 您需要为自定义播放头位置使用不同的值。
