---
description: TimeRangeCollection实用程序类抽象TimeRange规范有序集合的概念，并提供将自身转换为元数据实例的服务。
title: TimeRangecollection类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# TimeRangecollection类{#timerangecollection-class}

TimeRangeCollection实用程序类抽象TimeRange规范有序集合的概念，并提供将自身转换为元数据实例的服务。

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```java
public final class TimeRangeCollection {
    // default constructor method
    public TimeRangeCollection(Type type) {...}

    // the list of timerange specifications provided at construction time 
    public TimeRangeCollection(Type type, List<TimeRange> timeRanges) {...}

    // timerange specs can also be added later
    public void addTimeRange(TimeRange timeRange) {...}

    // translate the set of timerange specs into a Metadata instance 
    public Metadata toMetadata(Metadata options) {...}
}
```

此 `type` 参数是构造函数方法的签名中的第一个位置参数，是 `TimeRangeCollection#Type` 明细列表。 这是 `TimeRangeCollection` 类。 此枚举当前定义的值为 `MARK_RANGES`， `DELETE_RANGES`、和 `REPLACE_RANGES`. 您可以创建 `TimeRangeCollection` 对象使用这三种类型。
