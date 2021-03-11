---
description: 您可以在VOD内容中插入广告。
title: 用广告替换时间范围
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# 将时间范围替换为ad{#replace-time-ranges-with-an-ad}

您可以在VOD内容中插入广告。

在这种情况下，将从时间轴中删除`begin`和`end`之间的`TimeRanges`。 `localTime`它们由`begin`的`AdBreak`替换为`begin+replaceDuration`。 如果替换持续时间不作为参数存在，则服务器会对返回的Adbreak进行确定。

>[!NOTE]
>
>您应始终为自定义范围提供特定的替换持续时间。 如果没有用于替换此自定义范围的广告，则提供0的替换持续时间。

用Primetime广告决策广告替换范围。

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": 
              "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
                 
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 15000,
                    "replacement-duration": 15000 
                },
                {
                    "begin": 69000,
                    "end": 99000,
                    "replacement-duration": 30000
                },
                {
                    "begin": 251000,
                    "end": 281000,
                    "replacement-duration": 30000
                },
                {
                    "begin": 514000,
                    "end": 544000,
                    "replacement-duration": 30000
                } ]
            },
            "ad": {
                "targeting": [ {
                    "value": "MulAdsAvail12346",
                    "key": "osmfKeyMulAdsAvail12346"
                } ],
                "domain": "sandbox2.auditude.com",
                "mediaid": "psdk_000105",
                "zoneid": "121781"
            }     
        }
    },   
    "title": "VOD - Replace TimeRange with Auditude Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```

