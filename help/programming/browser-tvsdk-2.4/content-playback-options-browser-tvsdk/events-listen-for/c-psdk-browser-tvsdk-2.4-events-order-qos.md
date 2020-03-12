---
description: 浏览器TVSDK调度服务质量(QoS)事件，以通知您的应用程序可能影响QoS统计数据计算的事件，如缓冲和搜索事件。
seo-description: 浏览器TVSDK调度服务质量(QoS)事件，以通知您的应用程序可能影响QoS统计数据计算的事件，如缓冲和搜索事件。
seo-title: QoS事件
title: QoS事件
uuid: 3384bc51-b435-4cd9-a1f8-9abf2605205b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# QoS事件{#qos-events}

浏览器TVSDK调度服务质量(QoS)事件，以通知您的应用程序可能影响QoS统计数据计算的事件，如缓冲和搜索事件。

要获得所有QoS相关事件的通知，请创建MediaPlayer实 `AdobePSDK.QOSProvider` 例并将该实例附加到此实 `QOSProvider` 例：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

在应用程序中配置计时器以定期检查 `playbackInformation` 实例的属 `qosProvider` 性。 该属 `playbackInformation` 性提供当前播放统计信息的快照。 例如：

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

