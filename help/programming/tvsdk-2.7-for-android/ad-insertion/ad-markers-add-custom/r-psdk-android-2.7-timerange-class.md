---
description: 自定义广告标记允许您将表示时间轴区段的一组TimeRange规范传递给TVSDK。
seo-description: 自定义广告标记允许您将表示时间轴区段的一组TimeRange规范传递给TVSDK。
seo-title: TimeRange类
title: TimeRange类
uuid: e5a176af-29b9-4aa6-848e-5aba7988584b
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
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

