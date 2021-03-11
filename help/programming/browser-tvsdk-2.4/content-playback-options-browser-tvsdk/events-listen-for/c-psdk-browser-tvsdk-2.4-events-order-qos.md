---
description: 浏览器TVSDK调度服务质量(QoS)事件，以通知您的应用程序可能影响QoS统计数据计算的事件，如缓冲和搜索事件。
title: QoS事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# QoS事件{#qos-events}

浏览器TVSDK调度服务质量(QoS)事件，以通知您的应用程序可能影响QoS统计数据计算的事件，如缓冲和搜索事件。

要获得所有与QoS相关的事件的通知，请创建`AdobePSDK.QOSProvider`实例，并将MediaPlayer实例连接到此`QOSProvider`实例：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

在应用程序中配置计时器，以定期检查`qosProvider`实例的`playbackInformation`属性。 `playbackInformation`属性提供当前播放统计信息的快照。 例如：

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

