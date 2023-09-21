---
description: 浏览器TVSDK提供了用于分析和调试的量度。 您可以使用QoSProvider获取这些量度。
title: 量度
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# 量度{#metrics}

浏览器TVSDK提供了用于分析和调试的量度。 您可以使用QoSProvider获取这些量度。

例如：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```
