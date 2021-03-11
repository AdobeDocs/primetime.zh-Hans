---
description: 您可以将VOD内容中的时间间隔指定为广告中断。
title: 标记范围
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# 标记范围{#mark-ranges}

您可以将VOD内容中的时间间隔指定为广告中断。

在这种情况下，`localTime`中`begin`和`end`之间的`TimeRanges`将在时间轴中标记为`AdBreak`。 其他广告设置将被忽略。

>[!NOTE]
>
>如果您只想将内容中的特定范围标记为广告（无动态广告插入），请创建`CustomRangeMetadata`实例，并使用定义的自定义范围将类型指定为MARK操作。

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

