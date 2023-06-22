---
title: 特殊用例
description: 特殊用例
copied-description: true
exl-id: 33aad8cc-5939-4890-bc89-32d6bbf1fa4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 特殊用例{#special-use-cases}

TVSDK支持自定义范围设置，而不支持标准广告设置。 例如，如果定义了MARK范围，则会忽略广告的插入设置。 如果定义了REPLACE范围，TVSDK将自动使用 `CustomRanges` 信令模式。

1. `ReplaceRange` 无替换持续时间

   如果缺少更换持续时间，则实际更换持续时间由服务器确定。 在此投放的广告数 `AdBreak` 也由服务器决定。

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

1. 用替换持续时间标记和DELETE范围

   会忽略额外的替换持续时间。
