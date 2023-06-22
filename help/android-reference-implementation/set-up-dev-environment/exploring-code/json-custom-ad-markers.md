---
title: 自定义广告标记的JSON对象
description: 自定义广告标记的JSON对象
copied-description: true
exl-id: 85bcf306-703c-4a0d-b125-df9316fadf69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 自定义广告标记的JSON对象 {#json-object-for-custom-ad-markers}

当类型是自定义广告标记时，下面的代码块定义“详细信息”JSON对象。

IFeedItemAdapter：getStreamMetadata()返回的MetadataNode包含2个条目：
1. 具有类型键的项目 `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` 和返回的MetadataNode实例的值 `TimeRangeCollection.toMetadata()`.
1. 第二个条目具有类型键 `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` ，其值为 *adjust-seek-position* 属性。

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
| adjust-seek-position | true或false，用于设置MetadataNode中com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED键的值。 |
| 时间范围 | JSON对象数组，指示每个广告标记的时间范围。 每个JSON对象条目都映射到com.adobe.mediacore.utils.TimeRange的实例。 |
| time-ranges.begin | 以毫秒为单位的值，指示广告标记的开始时间。 |
| time-ranges.end | 以毫秒为单位的值，指示广告标记的结束时间。 |

有关自定义广告标记如何工作的更多信息，请参阅TVSDK文档。
