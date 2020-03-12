---
description: 您可以在VOD内容中插入广告。
seo-description: 您可以在VOD内容中插入广告。
seo-title: 用广告替换时间范围
title: 用广告替换时间范围
uuid: 8f09560c-bca3-4662-bc58-6c9cd0892476
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 用广告替换时间范围 {#replace-time-ranges-with-an-ad}

您可以在VOD内容中插入广告。

从时 `TimeRanges` 间轴中 `begin` 删 `end` 除和 `localTime` 中之间的内容。 这些范围将替换为 `AdBreak` 到 `begin` 的 `begin+replaceDuration`。 如果 `replacement-duration` 参数不存在，则服务器会对返回的内容做出确定 `Adbreak`。

>[!TIP]
>
>您应始终为自定义 `replacement-duration` 范围提供一个。 如果没有广告要替换此自定义范围，请提供 `replacement-duration` 0的广告。

1. 要用Primetime广告决策广告取代这些范围，请执行以下操作：

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [
               {
                   "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                   "type": "hls"
               }
           ],
           "metadata": {
               "time-ranges": {
                   "type": "replace",
                   "time-range-list": [
                       {
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
       "title": "VOD - Replace TimeRange with Auditude Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   }
   ```

