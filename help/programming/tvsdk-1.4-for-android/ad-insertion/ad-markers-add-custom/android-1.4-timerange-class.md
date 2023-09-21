---
description: 自定义广告标记允许您将表示时间线区段的一组TimeRange规范传递到TVSDK。
title: TimeRange类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# TimeRange类{#timerange-class}

自定义广告标记允许您将表示时间线区段的一组TimeRange规范传递到TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

集中的每个TimeRange规范都表示播放时间轴上的一个区段，该区段由TVSDK在内部维护，必须适当地标记为与广告相关的时段。

此 `TimeRange` 类是一种简单的数据结构，它公开时间轴上的开始位置和结束位置。 这两个只读属性抽象了播放时间轴中时间范围的概念。

>[!TIP]
>
>这两个值均以毫秒为单位表示。

以下是 `TimeRange` class：

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
