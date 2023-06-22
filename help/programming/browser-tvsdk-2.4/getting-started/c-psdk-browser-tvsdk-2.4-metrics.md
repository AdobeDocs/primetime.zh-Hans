---
description: 浏览器TVSDK提供用于分析和调试的量度。 您可以使用QoSProvider获取这些量度。
title: 量度
exl-id: 1413ddf5-b458-4040-abf8-8d9dbd6b80e2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# 量度{#metrics}

浏览器TVSDK提供用于分析和调试的量度。 您可以使用QoSProvider获取这些量度。

例如：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```
