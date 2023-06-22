---
description: 对于实时/线性内容，TVSDK会使用具有相同持续时间的广告时间替换主流内容的一个块，以便时间轴持续时间保持不变。
title: 实时/线性广告解析和插入
exl-id: b0fbdddf-8529-4f7a-aef2-1764320307f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# 实时/线性广告解析和插入{#live-linear-ad-resolving-and-insertion}

对于实时/线性内容，TVSDK会使用具有相同持续时间的广告时间替换主流内容的一个块，以便时间轴持续时间保持不变。

在播放之前和播放期间，TVSDK会解析已知广告，使用相同持续时间的广告时间替换主内容的各个部分，并在必要时重新计算虚拟时间轴。 广告时间的位置由清单定义的提示点指定。

TVSDK通过以下方式插入广告：

* **前置式广告**，位于内容的开头。
* **中置**，位于内容中间。

即使持续时间长于或短于提示点替换持续时间，TVSDK也会接受广告时间。 默认情况下，TVSDK支持 `#EXT-X-CUE` 提示在解决和放置广告时作为有效的广告标记。 此标记需要元数据字段 `DURATION` 以秒为单位，并且提示的唯一ID为。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>当实施常规 `AdPolicySelector`，可以为前置广告、中置广告和后置广告提供不同的策略 `AdBreakTimelineItem`s in `AdPolicyInfo`，它基于 `AdBreakTimelineItem`s.例如，您可以在播放中置内容后保留该内容，但可在播放前置内容后将其删除。

播放开始后，视频引擎会定期刷新清单文件。 当在清单中定义的实时流或线性流中遇到提示点时，TVSDK会解析任何新广告并插入广告。 解析和插入广告后，TVSDK会再次计算虚拟时间线并调度 `TimelineEvent.TIMELINE_UPDATED` 事件。
