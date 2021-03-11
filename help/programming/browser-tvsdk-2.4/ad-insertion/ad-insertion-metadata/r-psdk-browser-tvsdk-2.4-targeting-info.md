---
description: 在Adobe Primetime广告决策中，您可以目标关键值对上的广告。
title: 定位信息
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# 定位信息{#targeting-information}

在Adobe Primetime广告决策中，您可以目标关键值对上的广告。

要将这些键值对传递到浏览器TVSDK，请执行以下操作：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

