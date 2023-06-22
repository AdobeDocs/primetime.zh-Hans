---
description: 当您的播放包含广告时，浏览器TVSDK会按照通常预期的顺序发送事件/通知。 您的播放器可以按照预期顺序基于事件实施操作。
title: 广告事件的顺序
exl-id: fcc40aa8-9364-40a8-b2f2-9327e24819af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 广告事件的顺序{#order-of-advertising-events}

当您的播放包含广告时，浏览器TVSDK会按照通常预期的顺序发送事件/通知。 您的播放器可以按照预期顺序基于事件实施操作。

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

在播放广告时，事件的顺序为：

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* 将为广告时间中的每个广告调度以下内容：

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` （在广告播放期间多次）
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

以下示例显示了广告播放事件的典型进度：

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```
