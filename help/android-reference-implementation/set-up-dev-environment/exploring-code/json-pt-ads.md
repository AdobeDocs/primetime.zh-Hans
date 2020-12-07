---
seo-title: Primetime广告的JSON对象
title: Primetime广告的JSON对象
uuid: acf968d2-9856-4ed6-a046-1ac17d176571
description: 当类型值为Primetime广告时，以下代码块定义详细信息JSON对象。
seo-description: 当类型值为Primetime广告时，以下代码块定义详细信息JSON对象。
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Primetime广告的JSON对象{#json-object-for-primetime-ads}

当类型值为Primetime广告时，以下代码块定义详细信息JSON对象。

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
| 中介 | 在Primetime广告中为此内容设置的媒体。 |
| 宗 | Primetime广告zoneid。 有关更多信息，请参阅Primetime广告文档。 |
| 定位 | 用于定位内容特定广告的键／值对的数组。 |

有关这些属性值的详细信息，请参阅[com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html)。