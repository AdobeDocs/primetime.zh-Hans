---
description: 在某些分析实施中，客户端应用程序可能希望提供与TVSDK的localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于项目的播放时间提供每个开始的播放头。
seo-description: 在某些分析实施中，客户端应用程序可能希望提供与TVSDK的localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于项目的播放时间提供每个开始的播放头。
seo-title: 实施自定义时间更新
title: 实施自定义时间更新
uuid: 174937ca-3c26-4385-a298-8a01fc93ea20
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 实现自定义时间更新{#implement-custom-time-updates}

在某些分析实施中，客户端应用程序可能希望提供与TVSDK的localTime值报告的位置不同的播放头位置。 例如，在线性流播放期间，可以相对于项目的播放时间提供每个开始的播放头。

>[!TIP]
>
>仅当要提供与默认位置不同的播放头位置时，才覆盖此方法。

要覆盖默认播放头位置，请执行以下操作：

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>在此代码示例中，500只是示例值。 您需要为自定义播放头位置使用不同的值。