---
description: 自定义广告标记允许您将表示时间线段的一组TimeRange规范传递给TVSDK。
seo-description: 自定义广告标记允许您将表示时间线段的一组TimeRange规范传递给TVSDK。
seo-title: TimeRange类
title: TimeRange类
uuid: adf4f1ad-6b3b-48ac-a388-ee1fd54f770b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# TimeRange类{#timerange-class}

自定义广告标记允许您将表示时间线段的一组TimeRange规范传递给TVSDK。

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

集中的每个TimeRange规范都表示播放时间线上由TVSDK内部维护的段，且必须相应地标记为广告相关时段。

类是 `TimeRange` 一个简单的数据结构，它公开时间轴上的开始位置和结束位置。 这两个只读属性抽象了播放时间轴中某个时间范围的概念。

>[!TIP]
>
>这两个值以毫秒表示。

以下是课程的摘 `TimeRange` 要：

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

