---
description: 在某些分析实施中，客户端应用程序可能希望提供与浏览器TVSDK localTime值报告的位置不同的播放头位置。
seo-description: 在某些分析实施中，客户端应用程序可能希望提供与浏览器TVSDK localTime值报告的位置不同的播放头位置。
seo-title: 实施自定义时间更新
title: 实施自定义时间更新
uuid: 26a0592c-a47b-4d65-b984-5e51533dcddc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# 实现自定义时间更新{#implement-custom-time-updates}

在某些分析实施中，客户端应用程序可能希望提供与浏览器TVSDK localTime值报告的位置不同的播放头位置。

例如，在线性流播放期间，可以相对于项目的播放时间提供每个开始的播放头。

>[!TIP]
>
>仅当要提供除默认位置之外的播放头位置时，才覆盖此方法。

要覆盖默认播放头位置，请执行以下操作：

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>此代码片断中的值只是示例。 您需要对自定义播放头位置使用不同的值。

