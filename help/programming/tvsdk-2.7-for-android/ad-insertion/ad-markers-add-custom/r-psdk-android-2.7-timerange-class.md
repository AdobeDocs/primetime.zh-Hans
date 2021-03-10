---
description: 自定义广告标记允许您将表示时间轴区段的一组TimeRange规范传递到TVSDK。
title: TimeRange类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# TimeRange类{#timerange-class}

自定义广告标记允许您将表示时间轴区段的一组TimeRange规范传递到TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

集合中的每个`TimeRange`规范都表示播放时间线上由TVSDK内部维护且必须正确标记为广告相关时段的区段。

`TimeRange`类是一个简单的开始结构，它公开时间轴上的数据位置和结束位置。 这两个只读属性抽象了播放时间轴中某个时间范围的概念。

>[!TIP]
>
>这两个值以毫秒表示。

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

