---
description: 您可以从时间轴中以localTime的形式删除开始和结束之间的TimeRange。
seo-description: 您可以从时间轴中以localTime的形式删除开始和结束之间的TimeRange。
seo-title: 删除范围
title: 删除范围
uuid: 637829a7-efa8-4b83-9a04-ef01c043621f
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 删除范围{#delete-ranges}

您可以从时间轴中以localTime的形式删除开始和结束之间的TimeRange。

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

