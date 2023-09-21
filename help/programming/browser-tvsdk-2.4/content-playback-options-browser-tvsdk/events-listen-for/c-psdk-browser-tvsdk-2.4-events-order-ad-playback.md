---
description: 当您的播放包含广告时，浏览器TVSDK会按照通常预期的顺序发送事件/通知。 您的播放器可以按照预期顺序实施基于事件的操作。
title: 广告事件的顺序
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 广告事件的顺序{#order-of-advertising-events}

当您的播放包含广告时，浏览器TVSDK会按照通常预期的顺序发送事件/通知。 您的播放器可以按照预期顺序实施基于事件的操作。

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

在播放广告时，事件的顺序为：

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* 为广告时间中的每个广告调度以下内容：

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` （在广告播放期间多次）
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

以下示例显示了广告播放事件的典型进展：

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```
