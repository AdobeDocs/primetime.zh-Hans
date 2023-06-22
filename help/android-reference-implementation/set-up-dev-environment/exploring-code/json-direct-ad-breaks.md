---
title: 直接广告时间的JSON对象
description: 当类型值为直接广告时间时，详细介绍JSON对象
exl-id: d5e3ddd5-b963-4e7d-b04b-087d4fe96faf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 直接广告时间的JSON对象{#json-object-for-direct-ad-breaks}

当类型值为直接广告时间时，以下代码块定义了详细信息JSON对象。

此 `MetadataNode` 返回者 `IFeedItemAdapter:getStreamMetadata()` 包含具有类型键的条目 `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` 和值，该字符串表示以下详细信息JSON对象值。

```
“metadata”: { 
    “ad” :  { 
        “type”: “direct ad breaks”, 
        “details”: { 
            "ad-breaks": [ 
                { 
                    "tag": "break-001", 
                    "time": 0, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        }, 
                        { 
                        } 
                    ] 
                }, 
                { 
                    "tag": "break-002", 
                    "time": 300000, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        } 
                    ] 
                } 
            ] 
        } 
    } 
} 
```

| 属性 | 描述 |
|---|---|
| `tag` | 一个映射到中的标记字段的字符串 `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | 指示广告时间的开始时间，映射到中的时间字段 `com.adobe.mediacore.timeline.advertising.AdBreak`. 值为0表示前置广告。 |
| `replace` | 指示广告时间替换持续时间，映射到 `replaceDuration` 中的字段 `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | 在给定的广告时间内要播放的广告列表，映射到 `List<Ad>` 中的字段 `com.adobe.mediacore.timeline.advertising.AdBreak`. |

以下代码块为ads-list数组定义JSON对象。

```
"ad-list": [ 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 15000, 
        "tag": "1st break - 1st ad" 
    }, 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 30000, 
        "tag": "1st break - 2nd ad" 
    } 
], 
```

| 属性 | 描述 |
|---|---|
| `url` | 广告内容的URL，映射到中的url字段 `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | 广告的持续时间，映射到 `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | 描述字符串。 |
