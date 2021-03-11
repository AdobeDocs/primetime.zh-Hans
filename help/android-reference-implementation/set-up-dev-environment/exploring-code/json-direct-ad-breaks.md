---
title: 用于直接广告分段的JSON对象
description: 在类型值为直接和分段时详细列出JSON对象
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 直接广告分段的JSON对象{#json-object-for-direct-ad-breaks}

以下代码块定义当类型值为直接广告分段时的详细信息JSON对象。

`IFeedItemAdapter:getStreamMetadata()`返回的`MetadataNode`包含键类型为`com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY`的条目，以及下面详细JSON对象值的字符串表示形式的值。

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
| `tag` | 映射到`com.adobe.mediacore.timeline.advertising.AdBreak`中标记字段的字符串。 |
| `time` | 指示广告分段的开始时间，映射到`com.adobe.mediacore.timeline.advertising.AdBreak`中的时间字段。 值为0表示预置广告。 |
| `replace` | 指示广告中断替换持续时间，映射到`com.adobe.mediacore.timeline.advertising.AdBreak`中的`replaceDuration`字段。 |
| `ad-list` | 在给定广告分段期间要播放的广告列表，映射到`com.adobe.mediacore.timeline.advertising.AdBreak`中的`List<Ad>`字段。 |

以下代码块为ads-列表数组定义JSON对象。

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
| `url` | 广告内容的URL映射到`com.adobe.mediacore.timeline.advertising.Ad`中的url字段。 |
| `duration` | 广告的持续时间，映射到`com.adobe.mediacore.timeline.advertising.Ad`中的“持续时间”字段。 |
| `tag` | 描述字符串。 |

