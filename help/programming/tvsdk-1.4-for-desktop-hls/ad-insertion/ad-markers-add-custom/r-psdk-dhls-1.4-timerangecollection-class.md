---
description: TimeRangeCollection实用程序类抽象了TimeRange规范的有序集合的概念，并提供了将其自身转换为元数据实例的服务。
title: TimeRangeCollection类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# TimeRangeCollection类{#timerangecollection-class}

TimeRangeCollection实用程序类抽象了TimeRange规范的有序集合的概念，并提供了将其自身转换为元数据实例的服务。

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

集合类型的定义值为`MARK_RANGES`、`DELETE_RANGES`和`REPLACE_RANGES`。 可以使用这三种类型创建`TimeRangeCollection`。
