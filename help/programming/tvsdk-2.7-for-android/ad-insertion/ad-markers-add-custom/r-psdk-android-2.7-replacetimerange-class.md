---
description: ReplaceTimeRange实用程序类是要与CustomRangeMetadata一起使用的TimeRange类的扩展。
title: ReplaceTimeRange类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '36'
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

