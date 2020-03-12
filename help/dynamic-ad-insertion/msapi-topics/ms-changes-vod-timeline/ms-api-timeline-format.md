---
description: 您可以使用称为窗格的格式化广告和内容区段列表来指定或覆盖VOD内容中广告分段的时间轴。
seo-description: 您可以使用称为窗格的格式化广告和内容区段列表来指定或覆盖VOD内容中广告分段的时间轴。
seo-title: VOD时间轴格式
title: VOD时间轴格式
uuid: 6daaf605-e5ee-48dc-a222-a5973b3d915a
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# VOD时间轴格式 {#vod-timeline-format}

您可以使用称为窗格的格式化广告和内容区段列表来指定或覆盖VOD内容中广告分段的时间轴。

## 窗格 {#section_606E9456E25E41C8B8537A023DDD96CE}

窗格是广告中断或内容段。 时间轴由一系列窗格组成，各窗格之间用分号分隔。 存在以下类型的窗格：

### 广告中断

```
B,duration,maximum_number_of_ads,position
```

持续时间以秒为单位，精度为。001（毫秒）;广告数是整数。 职位如下：* **n** none — 无广告 ***** p-roll — 在内容* **m** Mid-roll之前— 内容* **t** Post-roll — 在内容之后

例如，在 `B,60,2,p` 内容发布前最多可分两个广告一分钟。

### 内容区段——章节

```
C,duration,number_of_lots
```

持续时间以秒为单位，精度为。001（毫秒）;批次数（内容部分）是整数。 例如， `C,300,1` 表示一个五分钟的内容部分。