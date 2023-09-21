---
description: 您可以在VOD内容中将时间间隔指定为广告时间。
title: 标记范围
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# 标记范围 {#mark-ranges}

您可以在VOD内容中将时间间隔指定为广告时间。

此 `TimeRanges` 介于 `begin` 和 `end` 在 `localTime` 将被标记为 `AdBreak` 在时间线中。 其他广告设置将被忽略。

>[!TIP]
>
>如果只想将内容中的某些范围标记为广告，而不想插入动态广告，请创建 `CustomRangeMetadata` 实例，并将类型指定为 `MARK` 操作中所定义的自定义范围。

1. 标记范围：

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
                   "type": "mark",
               "adjust-seek-position" : true,   
                   "time-range-list": [
                     {
                        "begin": 0,
                        "end": 15000
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
   
                 }
            }           
       },   
       "title": "VOD - MARK TimeRanges and no ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
          },
       "type": "vod",
       "id": "vod_004"
   }
   ```
