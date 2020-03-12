---
description: 您可以在VOD内容中插入广告。
seo-description: 您可以在VOD内容中插入广告。
seo-title: 用广告替换时间范围
title: 用广告替换时间范围
uuid: 50cdcc06-7df5-414b-95d4-c684bc68dce3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 用广告替换时间范围{#replace-time-ranges-with-an-ad}

您可以在VOD内容中插入广告。

在这种情况下， `TimeRanges` 将从时间 `begin` 轴 `end` 中移 `localTime` 除介于和in之间。 它们被替换为 `AdBreak` 的 `begin` 到 `begin+replaceDuration`。 如果替换持续时间不作为参数存在，则服务器会对返回的Adbreak做出确定。

>[!NOTE]
>
>您应始终为自定义范围提供特定的替换持续时间。 如果没有广告要替换此自定义范围，请提供替换持续时间为0的广告。

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

