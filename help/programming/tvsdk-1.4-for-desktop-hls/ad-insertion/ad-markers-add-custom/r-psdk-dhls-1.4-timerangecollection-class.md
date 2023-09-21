---
description: TimeRangeCollection实用程序类抽象TimeRange规范有序集合的概念，并提供将自身转换为元数据实例的服务。
title: TimeRangecollection类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---

# TimeRangecollection类{#timerangecollection-class}

TimeRangeCollection实用程序类抽象TimeRange规范有序集合的概念，并提供将自身转换为元数据实例的服务。

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

集合类型的已定义值为 `MARK_RANGES`， `DELETE_RANGES`、和 `REPLACE_RANGES`. 您可以创建 `TimeRangeCollection`使用这三种类型。
