---
description: 您可以使用名为pod的格式化的广告和内容区段列表，指定或覆盖VOD内容中广告时间的时间线。
title: VOD时间线格式
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# VOD时间线格式 {#vod-timeline-format}

您可以使用名为pod的格式化的广告和内容区段列表，指定或覆盖VOD内容中广告时间的时间线。

## Pod {#section_606E9456E25E41C8B8537A023DDD96CE}

面板是广告时间或内容区段。 时间轴包含一系列pod，以分号分隔。 存在以下类型的pod：

### 广告时间

```
B,duration,maximum_number_of_ads,position
```

持续时间以秒为单位，精度为。001（毫秒）；广告数是整数。 位置是以下位置之一：* **n** 无 — 无广告* **p** 前置式广告 — 内容之前* **m** 中置式广告 — 在内容中* **t** 后置式广告 — 内容之后

例如， `B,60,2,p` 表示在内容之前最多为2个广告设置一分钟的分隔时间。

### 内容区段 — 章节

```
C,duration,number_of_lots
```

持续时间以秒为单位，精度为。001 （毫秒）；批数（内容部分）是一个整数。 例如， `C,300,1` 表示内容的单个五分钟部分。