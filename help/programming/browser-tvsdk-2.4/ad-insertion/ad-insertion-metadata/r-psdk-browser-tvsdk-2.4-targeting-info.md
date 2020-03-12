---
description: 在Adobe Primetime广告决策中，您可以根据关键价值对定位广告。
seo-description: 在Adobe Primetime广告决策中，您可以根据关键价值对定位广告。
seo-title: 定位信息
title: 定位信息
uuid: 72114bef-36a1-4f2d-92e8-59f4885d70d2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 定位信息{#targeting-information}

在Adobe Primetime广告决策中，您可以根据关键价值对定位广告。

要将这些键值对传递到浏览器TVSDK，请执行以下操作：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

