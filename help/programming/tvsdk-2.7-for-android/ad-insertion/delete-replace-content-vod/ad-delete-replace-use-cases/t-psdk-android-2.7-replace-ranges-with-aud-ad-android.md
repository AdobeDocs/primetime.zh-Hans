---
description: 您可以在VOD内容中插入广告。
seo-description: 您可以在VOD内容中插入广告。
seo-title: 用广告替换时间范围
title: 用广告替换时间范围
uuid: 8f09560c-bca3-4662-bc58-6c9cd0892476
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 将时间范围替换为广告{#replace-time-ranges-with-an-ad}

您可以在VOD内容中插入广告。

`localTime`中`begin`和`end`之间的`TimeRanges`从时间轴中删除。 这些范围由`begin`到`begin+replaceDuration`的`AdBreak`替换。 如果`replacement-duration`不作为参数存在，则服务器将对返回的`Adbreak`进行确定。

>[!TIP]
>
>您应始终为自定义范围提供`replacement-duration`。 如果没有广告要替换此自定义范围，请提供`replacement-duration`，共0个。

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

