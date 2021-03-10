---
title: Primetime广告的JSON对象
description: 当类型值为Primetime广告时，下面的代码块定义详细信息JSON对象。
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Primetime广告{#json-object-for-primetime-ads}的JSON对象

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

| 属性 | 说明 |
|---|---|
| 域 | 用于广告请求的Primetime广告域。 |
| mediaid | 在Primetime广告中为此内容设置的媒体。 |
| zoneid | Primetime广告区域。 有关更多信息，请参阅Primetime广告文档。 |
| 定位 | 用于定位内容特定广告的键/值对的数组。 |

有关这些属性值的详细信息，请参阅[com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html)。