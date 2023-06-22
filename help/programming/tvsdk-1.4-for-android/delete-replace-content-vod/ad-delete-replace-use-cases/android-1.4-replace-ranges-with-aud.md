---
description: 您可以将广告插入VOD内容。
title: 用广告替换时间范围
exl-id: b341d337-e190-4e2d-bad6-579771bcc577
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# 用广告替换时间范围{#replace-time-ranges-with-an-ad}

您可以将广告插入VOD内容。

在这个案例中， `TimeRanges` 介于 `begin` 和 `end` 在 `localTime` 将从时间轴中删除。 它们将被替换为 `AdBreak` 之 `begin` 到 `begin+replaceDuration`. 如果replacement-duration不是作为参数存在，则服务器对返回的Adbreak进行确定。

>[!NOTE]
>
>您应始终为自定义范围提供特定的替换持续时间。 如果没有广告打算替换此自定义范围，请将替换持续时间设置为0。

将范围替换为Primetime广告和决策广告。

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
