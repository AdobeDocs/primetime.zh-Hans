---
title: 自定义广告标记的JSON对象
description: 自定义广告标记的JSON对象
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 自定义广告标记的JSON对象 {#json-object-for-custom-ad-markers}

当类型为自定义广告标记时，下面的代码块定义“详细信息”JSON对象。

IFeedItemAdapter：getStreamMetadata()返回的MetadataNode包含2个条目：
1. 具有类型键的条目 `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` 和返回的MetadataNode实例的值 `TimeRangeCollection.toMetadata()`.
1. 第二个条目具有类型键 `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 值为 *调整 — 搜寻 — 位置* 属性。

```
“metadata”: {
    “ad” :  {
        “type”: “custom ad markers”,
        “details”: {
            "adjust-seek-position": true,
            "time-ranges": [
                {
                    "begin": 5000,
                    "end":15000
                },
                {
                    "begin": 120000,
                    "end":135000
                }
            ]
        }
    }
}
```

| 属性 | 描述 |
|---|---|
| 调整 — 搜寻 — 位置 | true或false，用于设置MetadataNode中com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED键的值。 |
| 时间范围 | JSON对象数组，指示每个广告标记的时间范围。 每个JSON对象条目都映射到com.adobe.mediacore.utils.TimeRange的实例。 |
| time-ranges.begin | 指示广告标记开始时间的值（毫秒）。 |
| time-ranges.end | 指示广告标记结束时间的值（毫秒）。 |

有关自定义广告标记如何工作的更多信息，请参阅TVSDK文档。
