---
description: 浏览器TVSDK会调度服务质量(QoS)事件，以通知应用程序存在可能会影响QoS统计信息计算的事件，例如缓冲和搜寻事件。
title: QoS事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# QoS事件{#qos-events}

浏览器TVSDK会调度服务质量(QoS)事件，以通知应用程序存在可能会影响QoS统计信息计算的事件，例如缓冲和搜寻事件。

若要收到有关所有QoS相关事件的通知，请创建 `AdobePSDK.QOSProvider` 并将MediaPlayer实例附加到此 `QOSProvider` 实例：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

在应用程序中配置计时器，以定期检查 `playbackInformation` 的属性 `qosProvider` 实例。 此 `playbackInformation` 属性提供当前播放统计信息的快照。 例如：

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```
