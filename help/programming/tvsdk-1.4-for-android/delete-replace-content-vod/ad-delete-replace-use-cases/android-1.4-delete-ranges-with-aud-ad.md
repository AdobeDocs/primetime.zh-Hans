---
description: 您可以从时间轴中删除localTime中开始和结束之间的TimeRange。
seo-description: 您可以从时间轴中删除localTime中开始和结束之间的TimeRange。
seo-title: 删除范围
title: 删除范围
uuid: 2f4afa0d-69e3-4929-8dbd-b553c8a64d96
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 删除范围{#delete-ranges}

您可以从时间轴中删除localTime中开始和结束之间的TimeRange。

>[!NOTE]
>
>如果您只想从内容中删除某些范围，且广告映射必须按广告服务器的定义使用，请创建一个实例，然后使用定义的自定义范围将类型指定为DELETE操作。 `CustomRangeMetadata`

通过Adobe Primetime广告决策广告删除范围。

```
{   
    "properties": [],
    "stream": {
        "manifests": [
            {
                "url": "https://xyz.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                "type": "hls"
            }
        ],
     
        "metadata": {
            "time-ranges": {
                "type": "delete",
                "time-range-list": [
                    {
                        "begin": 0,
                        "end": 20000
                    },
                    {
                        "begin": 69000,
                        "end": 99000
                    },
                    {
                        "begin": 251000,
                        "end": 281000
                    },
                    {
                        "begin": 514000,
                        "end": 544000
                    }
                ]
     
            },
            "ad": {
                "targeting": [
                    {
                        "value": "MulAdsAvail12346",
                        "key": "osmfKeyMulAdsAvail12346"
                    }
                ],
                "domain": "sandbox2.auditude.com",
                "mediaid": "psdk_000105",
                "zoneid": "121781"
            }     
        }
    },   
    "title": "VOD - DELETE TimeRange with Primetime ad decisioning Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```

