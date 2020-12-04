---
description: ReplaceTimeRange实用程序类是要与CustomRangeMetadata一起使用的TimeRange类的扩展。
seo-description: ReplaceTimeRange实用程序类是要与CustomRangeMetadata一起使用的TimeRange类的扩展。
seo-title: ReplaceTimeRange类
title: ReplaceTimeRange类
uuid: d554c17a-2bdc-4c4a-bb8f-2d357511bb32
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---


# ReplaceTimeRange类{#replacetimerange-class}

ReplaceTimeRange实用程序类是要与CustomRangeMetadata一起使用的TimeRange类的扩展。

```java
public class ReplaceTimeRange extends TimeRange {
    // Default constructor method
    public ReplaceTimeRange() { 
        ... 
    }

    // Details of begining, duration and replaceDuration 
    // provided at construction time 
    public ReplaceTimeRange(long begin, long duration, long replaceDuration) { 
        ... 
    }

    // Replace duration
    public long getReplaceDuration() { 
        ... 
    }
}
```
