---
description: ReplaceTimeRange实用程序类是要与CustomRangeMetadata一起使用的TimeRange类的扩展。
seo-description: ReplaceTimeRange实用程序类是要与CustomRangeMetadata一起使用的TimeRange类的扩展。
seo-title: ReplaceTimeRange类
title: ReplaceTimeRange类
uuid: 19c49b26-5096-4429-b30b-bdd2502e3036
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# ReplaceTimeRange类 {#replacetimerange-class}

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

