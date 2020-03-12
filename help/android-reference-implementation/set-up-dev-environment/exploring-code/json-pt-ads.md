---
seo-title: 用于Primetime广告的JSON对象
title: 用于Primetime广告的JSON对象
uuid: acf968d2-9856-4ed6-a046-1ac17d176571
description: 以下代码块定义当类型值为Primetime广告时的详细JSON对象。
seo-description: 以下代码块定义当类型值为Primetime广告时的详细JSON对象。
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 用于Primetime广告的JSON对象 {#json-object-for-primetime-ads}

以下代码块定义当类型值为Primetime广告时的详细JSON对象。

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
| zoneid | Primetime广告zoneid。 有关更多信息，请参阅Primetime广告文档。 |
| 定位 | 一组键／值对，用于定位内容的特定广告。 |

有 [关这些属性值的详细信息](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) ，请参阅com.adobe.mediacore.metadata.AuditudeSettings。