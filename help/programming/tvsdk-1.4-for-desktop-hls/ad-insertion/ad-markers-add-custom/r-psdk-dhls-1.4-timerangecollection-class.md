---
description: TimeRangeCollection实用程序类抽象TimeRange规范有序集合的概念，并提供将自身转换为元数据实例的服务。
title: TimeRangecollection类
exl-id: 2e5160b0-2254-4a40-8c32-fe3e05b9fc30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

集合类型的定义值为 `MARK_RANGES`， `DELETE_RANGES`、和 `REPLACE_RANGES`. 您可以创建 `TimeRangeCollection`使用这三种类型。
