---
title: 适用于Primetime广告的JSON对象
description: 当类型值为Primetime广告时，下面的代码块定义详细信息JSON对象。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 适用于Primetime广告的JSON对象 {#json-object-for-primetime-ads}

当类型值为Primetime广告时，下面的代码块定义详细信息JSON对象。

```
“metadata”: {
    “ad” :  {
        “type”: “Primetime ads”,
        “details”: {
            "domain": "sandbox2.auditude.com",
            "mediaid": "rom_asset_case_1",
            "zoneid": "109754",
            "targeting": [
                {
                    "key": "osmfKeyMulAdsAvail12346",
                    "value": "MulAdsAvail12346"
                }
            ]
        }
    }
}
```

| 属性 | 描述 |
|---|---|
| 域 | 用于广告请求的Primetime广告域。 |
| mediaid | Primetime中已为此内容设置的Mediaid广告。 |
| zoneid | Primetime广告zoneid。 有关更多信息，请参阅Primetime广告文档。 |
| 定位 | 键/值对数组，用于定位内容的特定广告。 |

请参阅 [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) 以了解有关这些属性的值的更多信息。
