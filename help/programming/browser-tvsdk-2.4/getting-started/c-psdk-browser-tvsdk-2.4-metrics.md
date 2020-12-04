---
description: 浏览器TVSDK提供用于分析和调试的指标。 您可以使用QoSProvider获得这些指标。
seo-description: 浏览器TVSDK提供用于分析和调试的指标。 您可以使用QoSProvider获得这些指标。
seo-title: 指标
title: 指标
uuid: 4734e532-1f83-4691-b1bd-785f78e55d8d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 3%

---


# 度量{#metrics}

浏览器TVSDK提供用于分析和调试的指标。 您可以使用QoSProvider获得这些指标。

例如：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

