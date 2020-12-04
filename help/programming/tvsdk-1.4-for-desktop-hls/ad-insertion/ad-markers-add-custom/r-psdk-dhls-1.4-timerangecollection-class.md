---
description: TimeRangeCollection实用程序类抽象出TimeRange规范的有序集合的概念，并提供服务将其转换为元数据实例。
seo-description: TimeRangeCollection实用程序类抽象出TimeRange规范的有序集合的概念，并提供服务将其转换为元数据实例。
seo-title: TimeRangeCollection类
title: TimeRangeCollection类
uuid: da781df4-6b19-47e1-8dc5-ea83c139f061
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# TimeRangeCollection类{#timerangecollection-class}

TimeRangeCollection实用程序类抽象出TimeRange规范的有序集合的概念，并提供服务将其转换为元数据实例。

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
