---
description: 您可以从时间轴中以localTime的形式删除开始和结束之间的TimeRange。
seo-description: 您可以从时间轴中以localTime的形式删除开始和结束之间的TimeRange。
seo-title: 删除范围
title: 删除范围
uuid: 2aaea7a0-5d52-49a1-901c-f71e4b081d91
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# 删除范围{#delete-ranges}

您可以从时间轴中删除`begin`和`end`之间的`TimeRanges`。`localTime`

>[!TIP]
>
>要仅从内容中删除某些范围，请创建`CustomRangeMetadata`实例，并使用定义的自定义范围将类型指定为`DELETE`操作。

广告映射必须由广告服务器定义。

1. 要通过Adobe Primetime广告决策广告删除范围，请执行以下操作：

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
       "title": "VOD - DELETE TimeRange with xm-replace_text Phrase Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   },
   ```
