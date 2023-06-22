---
title: Primetime广告的JSON对象
description: 当类型值为Primetime广告时，下面的代码块定义详细信息JSON对象。
exl-id: b1392781-2dfb-4934-b1ce-1c761cbfb22d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Primetime广告的JSON对象 {#json-object-for-primetime-ads}

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
| mediaid | Primetime中为此内容设置的Mediaid广告。 |
| zoneid | Primetime广告zoneid。 有关更多信息，请参阅Primetime广告文档。 |
| 定位 | 用于为内容定位特定广告的键/值对数组。 |

参见 [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) 以了解有关这些属性的值的更多信息。
