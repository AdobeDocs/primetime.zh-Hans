---
description: 您可以使用称为窗格的广告和内容区段的格式化列表来指定或覆盖VOD内容中广告分段的时间轴。
seo-description: 您可以使用称为窗格的广告和内容区段的格式化列表来指定或覆盖VOD内容中广告分段的时间轴。
seo-title: VOD时间轴格式
title: VOD时间轴格式
uuid: 6daaf605-e5ee-48dc-a222-a5973b3d915a
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# VOD时间线格式{#vod-timeline-format}

您可以使用称为窗格的广告和内容区段的格式化列表来指定或覆盖VOD内容中广告分段的时间轴。

## 窗格{#section_606E9456E25E41C8B8537A023DDD96CE}

窗格是广告中断或内容段。 时间轴由一系列窗格组成，以分号分隔。 存在以下类型的窗格：

### 广告中断

```
B,duration,maximum_number_of_ads,position
```

持续时间以秒为单位，精度为。001（毫秒）;广告数是整数。 职位是以下任一项：
* **n**无——无广告
* **p**预卷——在内容之前
* **m**中间卷——在内容中
* **t**&#x200B;后置——在内容发布后

例如，`B,60,2,p`表示内容前最多2个广告的分隔一分钟。

### 内容区段——章节

```
C,duration,number_of_lots
```

持续时间以秒为单位，精度为。001（毫秒）;批次数（内容部分）是整数。 例如，`C,300,1`表示一个五分钟的内容部分。