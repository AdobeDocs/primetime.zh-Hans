---
seo-title: 自定义广告标记的JSON对象
title: 自定义广告标记的JSON对象
uuid: 2c05d9ce-a22f-4829-bfea-9dcf0dc7cd6d
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 自定义广告标记的JSON对象 {#json-object-for-custom-ad-markers}

当类型为自定义广告标记时，以下代码块定义“详细信息”JSON对象。

IFeedItemAdapter:getStreamMetadata()返回的MetadataNode包含2个条目：
1. 一个条目，其类型 `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` 和值为返回的MetadataNode实例的键 `TimeRangeCollection.toMetadata()`。
1. 第二个条目具有类型键， `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 其值为下 *面的adjust-seek-position* 属性。

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

| 属性 | 说明 |
|---|---|
| 调整搜索位置 | true或false，用于在MetadataNode中设置com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED键的值。 |
| 时间范围 | 指示每个广告标记的时间范围的JSON对象数组。 每个JSON对象条目都映射到com.adobe.mediacore.utils.TimeRange的一个实例。 |
| time-ranges.begin | 以毫秒为单位的值，表示广告标记的开始时间。 |
| time-ranges.end | 指示广告标记结束时间的毫秒值。 |

有关自定义广告标记如何工作的更多信息，请参阅TVSDK文档。
