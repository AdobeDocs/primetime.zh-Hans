---
description: TimeRangeCollection实用程序类抽象出TimeRange规范的有序集合的概念，并提供服务将其转换为元数据实例。
seo-description: TimeRangeCollection实用程序类抽象出TimeRange规范的有序集合的概念，并提供服务将其转换为元数据实例。
seo-title: TimeRangeCollection类
title: TimeRangeCollection类
uuid: 5705dc9d-4325-44b0-b5aa-196d09c3a67e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---


# TimeRangeCollection类{#timerangecollection-class}

TimeRangeCollection实用程序类抽象出TimeRange规范的有序集合的概念，并提供服务将其转换为元数据实例。

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

`type`参数是构造函数方法签名中的第一个位置参数，是`TimeRangeCollection#Type`明细列表的实例。 这是`TimeRangeCollection`类的一部分。 此明细列表当前定义的值为`MARK_RANGES`、`DELETE_RANGES`和`REPLACE_RANGES`。 可以使用这三种类型创建`TimeRangeCollection`对象。
