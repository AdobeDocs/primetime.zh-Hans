---
description: TimeRangeCollection实用程序类抽象了TimeRange规范的有序集合的概念，并提供了将其自身转换为元数据实例的服务。
title: TimeRangeCollection类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# TimeRangeCollection类{#timerangecollection-class}

TimeRangeCollection实用程序类抽象了TimeRange规范的有序集合的概念，并提供了将其自身转换为元数据实例的服务。

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

`type`参数是构造函数方法签名中的第一个位置参数，是`TimeRangeCollection#Type`明细列表的实例。 这是`TimeRangeCollection`类的一部分。 此明细列表当前定义的值为`MARK_RANGES`、`DELETE_RANGES`和`REPLACE_RANGES`。 您可以使用这三种类型创建`TimeRangeCollection`对象。
