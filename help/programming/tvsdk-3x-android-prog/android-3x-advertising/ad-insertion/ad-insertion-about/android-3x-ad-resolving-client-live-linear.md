---
description: 对于实时/线性内容，TVSDK会使用具有相同持续时间的广告时间替换主流内容的一个块，以便时间轴持续时间保持不变。
title: 解析和插入实时/线性广告
exl-id: 2097520f-283b-4839-af5e-b1cfb0f3f359
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 解析和插入实时/线性广告 {#resolve-and-insert-live-linear-ad}

对于实时/线性内容，TVSDK会使用具有相同持续时间的广告时间替换主流内容的一个块，以便时间轴持续时间保持不变。

在播放之前和播放期间，TVSDK会解析已知广告，使用相同持续时间的广告时间替换主内容的各个部分，并在必要时重新计算虚拟时间轴。 广告时间的位置由清单定义的提示点指定。

TVSDK通过以下方式插入广告：

* **前置式广告**，放在内容之前。
* **中置**，该文件放在内容的中间。

即使持续时间长于或短于提示点替换持续时间，TVSDK也会接受广告时间。 默认情况下，TVSDK支持 `#EXT-X-CUE` 提示在解决和放置广告时作为有效的广告标记。 此标记需要元数据字段 `DURATION` 以秒为单位表示的值和提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定义并订阅其他提示（标记）。

播放开始后，视频引擎会定期刷新清单文件。 当在清单中定义的实时流或线性流中遇到提示点时，TVSDK会解析任何新广告并插入广告。 解析和插入广告后，TVSDK会再次计算虚拟时间线并调度 `TimelineItemsUpdatedEventListener.onTimelineUpdated` 事件。
