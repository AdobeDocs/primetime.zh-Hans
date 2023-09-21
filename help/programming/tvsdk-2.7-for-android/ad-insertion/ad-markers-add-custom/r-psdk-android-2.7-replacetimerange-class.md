---
description: ReplaceTimeRange实用程序类是与CustomRangeMetadata一起使用的TimeRange类的扩展。
title: ReplaceTimeRange类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 0%

---

# ReplaceTimeRange类 {#replacetimerange-class}

ReplaceTimeRange实用程序类是与CustomRangeMetadata一起使用的TimeRange类的扩展。

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
