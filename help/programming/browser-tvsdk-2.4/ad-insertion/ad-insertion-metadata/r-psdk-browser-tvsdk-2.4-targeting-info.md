---
description: 在Adobe Primetime ad decisioning中，您可以在键值对上定位广告。
title: 定位信息
exl-id: 25610f7d-6b14-4ed1-b61c-9e6bf13ba8e6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 定位信息{#targeting-information}

在Adobe Primetime ad decisioning中，您可以在键值对上定位广告。

要将这些键值对传递到浏览器TVSDK，请执行以下操作：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```
