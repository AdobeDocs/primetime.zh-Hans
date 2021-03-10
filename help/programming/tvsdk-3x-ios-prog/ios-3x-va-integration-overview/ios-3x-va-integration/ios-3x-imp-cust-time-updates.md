---
description: 在某些分析实施中，客户端应用程序可能希望提供与TVSDK的localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于每个项目的开始时间提供每个数据的播放头。
title: 实施自定义时间更新
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# 实现自定义时间更新{#implement-custom-time-updates}

在某些分析实施中，客户端应用程序可能希望提供与TVSDK的localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于每个项目的开始时间提供每个数据的播放头。

>[!TIP]
>
>仅当要提供与默认位置不同的播放头位置时，才覆盖此方法。

要覆盖默认播放指示器位置，请执行以下操作：

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>在此代码示例中，500只是示例值。 您需要对自定义播放头位置使用不同的值。