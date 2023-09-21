---
title: 特殊用例
description: 特殊用例
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 特殊用例{#special-use-cases}

TVSDK支持自定义范围设置，而不支持标准广告设置。 例如，如果定义了MARK范围，则会忽略广告的插入设置。 如果定义了REPLACE范围，TVSDK将自动使用 `CustomRanges` 信令模式。

1. `ReplaceRange` 无替换持续时间

   如果缺少更换持续时间，则实际更换持续时间由服务器决定。 在此投放的广告数 `AdBreak` 也由服务器决定。

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

1. 标记和DELETE包含替换持续时间的范围

   会忽略额外的替换持续时间。
