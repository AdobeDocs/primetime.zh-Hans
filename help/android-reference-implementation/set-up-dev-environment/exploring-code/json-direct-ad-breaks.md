---
seo-title: 用于直接广告中断的JSON对象
title: 用于直接广告中断的JSON对象
uuid: ffb901f4-0a8b-40fe-b6ba-5ffebc324cf2
description: 在类型值为直接和分段时详细描述JSON对象
seo-description: 在类型值为直接和分段时详细描述JSON对象
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 用于直接广告中断的JSON对象{#json-object-for-direct-ad-breaks}

以下代码块定义当类型值为直接分段时的详细信息JSON对象。

返回 `MetadataNode` 的包 `IFeedItemAdapter:getStreamMetadata()` 含一个条目，其中包含类型和值的键， `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` 以下是详细JSON对象值的字符串表示形式。

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

| 属性 | 说明 |
|---|---|
| `tag` | 映射到中标记字段的字符串 `com.adobe.mediacore.timeline.advertising.AdBreak`。 |
| `time` | 指示广告中断的开始时间，映射到中的时间字段 `com.adobe.mediacore.timeline.advertising.AdBreak`。 值为0表示预先滚动广告。 |
| `replace` | 指示广告中断替换持续时间，映射到中 `replaceDuration` 的字段 `com.adobe.mediacore.timeline.advertising.AdBreak`。 |
| `ad-list` | 给定广告分时段内要播放的广告列表，映射到中 `List<Ad>` 的字段 `com.adobe.mediacore.timeline.advertising.AdBreak`。 |

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

| 属性 | 说明 |
|---|---|
| `url` | 广告内容的URL，映射到中的url字段 `com.adobe.mediacore.timeline.advertising.Ad`。 |
| `duration` | 广告的持续时间，映射到中的持续时间字段 `com.adobe.mediacore.timeline.advertising.Ad`。 |
| `tag` | 描述字符串。 |

