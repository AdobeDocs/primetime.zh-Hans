---
description: 您可以将VOD内容中的时间间隔指定为广告分段。
seo-description: 您可以将VOD内容中的时间间隔指定为广告分段。
seo-title: 标记范围
title: 标记范围
uuid: 6ae2adee-fb7a-4cef-a8e8-ecf671ed3660
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 标记范围 {#mark-ranges}

您可以将VOD内容中的时间间隔指定为广告分段。

在 `TimeRanges` 和之 `begin` 间 `end` 的内 `localTime` 容将在时间轴 `AdBreak` 中标记为。 其他广告设置将被忽略。

>[!TIP]
>
>如果只要将内容中的特定范围标记为广告，而不需要动态广告插入，请创建一个实例，然后使用定义的自定义范围将类型指 `CustomRangeMetadata``MARK` 定为操作。

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

