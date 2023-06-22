---
description: 您可以将VOD内容中的时间间隔指定为广告时间。
title: 标记范围
exl-id: cd661327-20b2-4a49-8002-6ecee86c2a2c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 标记范围{#mark-ranges}

您可以将VOD内容中的时间间隔指定为广告时间。

在这个案例中， `TimeRanges` 介于 `begin` 和 `end` 在 `localTime` 将被标记为 `AdBreak` 在时间轴中。 其他广告设置将被忽略。

>[!NOTE]
>
>如果只想将内容中的某些范围标记为广告（不插入动态广告），请创建 `CustomRangeMetadata` 实例，并将类型指定为具有定义的自定义范围的MARK操作。

1. 标记范围。

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "time-ranges": {
                   "type": "mark",
                   "adjust-seek-position" : true,   
                   "time-range-list": [ {
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
                    } ]
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
