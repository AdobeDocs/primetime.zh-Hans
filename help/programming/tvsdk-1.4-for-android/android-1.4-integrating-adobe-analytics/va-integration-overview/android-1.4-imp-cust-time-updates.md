---
description: 在某些分析实施中，客户端应用程序可能希望提供与TVSDK localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于项目的播放时间提供每个开始的播放头。
seo-description: 在某些分析实施中，客户端应用程序可能希望提供与TVSDK localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于项目的播放时间提供每个开始的播放头。
seo-title: 实施自定义时间更新
title: 实施自定义时间更新
uuid: 7f5d46e5-eab6-4bdc-b015-ae27ddb609ce
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# 实现自定义时间更新{#implement-custom-time-updates}

在某些分析实施中，客户端应用程序可能希望提供与TVSDK localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于项目的播放时间提供每个开始的播放头。

>[!TIP]
>
>仅当要提供除默认位置之外的播放头位置时，才覆盖此方法。

要覆盖默认播放头位置，请执行以下操作：

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
>此代码片断中的值只是示例。 您需要对自定义播放头位置使用不同的值。