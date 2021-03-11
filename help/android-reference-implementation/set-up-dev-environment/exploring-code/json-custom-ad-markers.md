---
title: 自定义广告标记的JSON对象
description: 自定义广告标记的JSON对象
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 自定义广告标记{#json-object-for-custom-ad-markers}的JSON对象

当类型为自定义广告标记时，下面的代码块定义“详细信息”JSON对象。

IFeedItemAdapter:getStreamMetadata()返回的MetadataNode包含2个条目：
1. 键类型为`com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY`的条目，以及由`TimeRangeCollection.toMetadata()`返回的MetadataNode实例的值。
1. 第二条目具有类型`com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED`的键，其值为下面的&#x200B;*adjust-seek-position*&#x200B;属性。

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
| 调整搜索位置 | true或false，用于设置MetadataNode中com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED键的值。 |
| 时间范围 | 指示每个广告标记的时间范围的JSON对象数组。 每个JSON对象条目都映射到com.adobe.mediacore.utils.TimeRange的实例。 |
| time-ranges.begin | 指示广告标记开始时间的毫秒值。 |
| time-ranges.end | 指示广告标记结束时间的毫秒值。 |

有关自定义广告标记如何工作的更多信息，请参阅TVSDK文档。
