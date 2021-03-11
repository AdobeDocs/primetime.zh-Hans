---
description: 您可以使用称为窗格的广告和内容区段的格式化列表来指定或覆盖VOD内容中广告分段的时间线。
title: VOD时间轴格式
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# VOD时间轴格式{#vod-timeline-format}

您可以使用称为窗格的广告和内容区段的格式化列表来指定或覆盖VOD内容中广告分段的时间线。

## 窗格{#section_606E9456E25E41C8B8537A023DDD96CE}

窗格是广告中断或内容区段。 时间轴由一系列窗格组成，以分号分隔。 存在以下类型的窗格：

### 广告中断

```
B,duration,maximum_number_of_ads,position
```

持续时间以秒为单位，精度为。001（毫秒）；广告数是整数。 职位如下：
* **n**无 — 无广告
* **p**预卷 — 内容之前
* **m**中间版 — 在内容中
* **t**&#x200B;售后 — 在内容之后

例如，`B,60,2,p`表示内容前最多2个广告的1分钟休息时间。

### 内容区段 — 章节

```
C,duration,number_of_lots
```

持续时间以秒为单位，精度为。001（毫秒）；批次数（内容部分）是整数。 例如，`C,300,1`表示一个五分钟的内容部分。