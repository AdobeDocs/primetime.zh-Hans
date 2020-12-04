---
description: 您可以将VOD内容中的时间间隔指定为广告分段。
seo-description: 您可以将VOD内容中的时间间隔指定为广告分段。
seo-title: 标记范围
title: 标记范围
uuid: fa6047dc-9a12-42fa-9e58-8ee3a55fa866
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# 标记范围{#mark-ranges}

您可以将VOD内容中的时间间隔指定为广告分段。

`localTime`中`begin`和`end`之间的`TimeRanges`将在时间轴中标记为`AdBreak`。 其他广告设置将被忽略。

>[!TIP]
>
>如果只要将内容中的特定范围标记为广告，而不需要动态广告插入，请创建`CustomRangeMetadata`实例，并使用定义的自定义范围将类型指定为`MARK`操作。

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
