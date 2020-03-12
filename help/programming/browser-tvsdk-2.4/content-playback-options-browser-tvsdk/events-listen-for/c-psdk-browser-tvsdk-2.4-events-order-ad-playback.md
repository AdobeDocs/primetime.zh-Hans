---
description: 当您的播放包括广告时，Browser TVSDK会按通常预期的序列发送事件／通知。 播放器可以根据预期序列中的事件执行操作。
seo-description: 当您的播放包括广告时，Browser TVSDK会按通常预期的序列发送事件／通知。 播放器可以根据预期序列中的事件执行操作。
seo-title: 广告活动的顺序
title: 广告活动的顺序
uuid: 9787e6ac-5e52-4d7d-8fc7-f7609633707c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 广告活动的顺序{#order-of-advertising-events}

当您的播放包括广告时，Browser TVSDK会按通常预期的序列发送事件／通知。 播放器可以根据预期序列中的事件执行操作。

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

播放广告时，事件的顺序是：

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* 为广告中断中的每个广告分派以下内容：

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

