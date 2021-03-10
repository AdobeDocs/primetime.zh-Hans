---
description: 当您的播放包括广告时，Browser TVSDK会按通常预期的序列调度事件/通知。 您的播放器可以根据预期序列中的事件来实施操作。
title: 广告事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 广告事件的顺序{#order-of-advertising-events}

当您的播放包括广告时，Browser TVSDK会按通常预期的序列调度事件/通知。 您的播放器可以根据预期序列中的事件来实施操作。

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

播放广告时，事件的顺序是：

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* 在广告分段中，将为每个广告分派以下内容：

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` （在广告播放期间多次）
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

以下示例展示了广告播放事件的典型进度：

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```

