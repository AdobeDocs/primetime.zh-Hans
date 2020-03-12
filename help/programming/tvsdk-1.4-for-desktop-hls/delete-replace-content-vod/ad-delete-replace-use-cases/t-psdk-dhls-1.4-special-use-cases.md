---
description: 'null'
seo-description: 'null'
seo-title: 特殊用例
title: 特殊用例
uuid: 066bc256-4fdf-4083-b23e-0a916b3b532f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 特殊用例{#special-use-cases}

TVSDK偏好自定义范围设置而不是标准广告设置。 例如，如果定义了MARK范围，则忽略广告的插入设置。 如果定义了REPLACE范围，则TVSDK会自动使用信 `CustomRanges` 令模式。

1. `ReplaceRange` 无需更换持续时间

   如果缺少替换持续时间，则实际替换持续时间由服务器确定。 放入此广告的数 `AdBreak` 量也由服务器决定。

   ```
   {
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://. . ./vanilla/index.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "signaling-mode": "custom time ranges",
               "time-ranges": {
                   "type": "replace",
                   "adjust-seek-position": true,
                   "time-range-list": [{
                   "begin": 0,
                   "end": 30000
               }, {
                   "begin": 60000,
                   "end": 75000
               }, {
                   "begin": 255000,
                   "end": 300000
               } ]
               },
               "ad": {             
                   "domain": "sandbox2.auditude.com",
                   "mediaid": "psdk_000105",
                   "zoneid": "121781"
               }     
           }
       },
       "title": "Verify 30Sec Pre-Roll, 15 Sec Mid roll Ad and 
       45 second Post-Roll can be replaced in one shot.",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_001"
   }
   ```

1. 具有替换持续时间的标记和删除范围

   将忽略额外的替换持续时间。
