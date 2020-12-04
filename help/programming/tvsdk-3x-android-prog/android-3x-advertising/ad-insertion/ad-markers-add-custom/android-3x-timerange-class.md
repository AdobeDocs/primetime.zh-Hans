---
description: 自定义广告标记允许您将表示时间轴区段的一组TimeRange规范传递给TVSDK。
seo-description: 自定义广告标记允许您将表示时间轴区段的一组TimeRange规范传递给TVSDK。
seo-title: TimeRange类
title: TimeRange类
uuid: af3ce5e6-44b5-457f-a6e7-aa232defb91e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# TimeRange类{#timerange-class}

自定义广告标记允许您将表示时间轴区段的一组TimeRange规范传递给TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

集合中的每个`TimeRange`规范都表示播放时间线上由TVSDK内部维护的段，该段必须相应地标记为与广告相关的段。

`TimeRange`类是一个简单的数据结构，它在时间线上显示开始位置和结束位置。 这两个只读属性抽象了播放时间轴中某个时间范围的概念。

>[!TIP]
>
>这两个值以毫秒为单位表示。

以下是`TimeRange`类的摘要：

```java
public final class TimeRange {
    // the start/end values are provided at construction time
    public static TimeRange createRange(long begin, long duration) {...} 

    // only getters are available
    public long getBegin() {...} 
    public long getEnd() {...} 
    public long getDuration() {...}
}
```
