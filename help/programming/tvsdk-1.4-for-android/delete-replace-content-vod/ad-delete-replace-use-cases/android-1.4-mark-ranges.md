---
description: 您可以将VOD内容中的时间间隔指定为广告分段。
seo-description: 您可以将VOD内容中的时间间隔指定为广告分段。
seo-title: 标记范围
title: 标记范围
uuid: eb99a1c2-6c0c-40a4-bac2-98dce45acfad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 标记范围{#mark-ranges}

您可以将VOD内容中的时间间隔指定为广告分段。

在这种情况下， `TimeRanges` 在和 `begin` 中之间 `end` 将标 `localTime` 记为时间轴 `AdBreak` 中的一个。 其他广告设置将被忽略。

>[!NOTE]
>
>如果您只想将内容中的特定范围标记为广告（无动态广告插入），请创建一个实例，然后使用定义的自定义范围将类型指定为MARK操作。 `CustomRangeMetadata`

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

