---
description: 您可以从时间线中移除localTime中开始和结束时间之间的TimeRanges。
title: 删除范围
exl-id: a91cd7ac-d60f-43bb-a783-ccc1b9b9e7fd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# 删除范围{#delete-ranges}

您可以从时间线中移除localTime中开始和结束时间之间的TimeRanges。

>[!TIP]
>
>要仅从内容中删除某些范围，请创建 `CustomRangeMetadata` 实例并将类型指定为 `DELETE` 使用定义的自定义范围执行操作。

广告映射的使用方式必须如广告服务器所定义。

1. 要删除包含Adobe Primetime ad decisioning广告的范围：

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
