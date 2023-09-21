---
description: 在Adobe Primetime ad decisioning中，您可以定位键值对上的广告。
title: 定位信息
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 定位信息{#targeting-information}

在Adobe Primetime ad decisioning中，您可以定位键值对上的广告。

要将这些键值对传递到浏览器TVSDK，请执行以下操作：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```
