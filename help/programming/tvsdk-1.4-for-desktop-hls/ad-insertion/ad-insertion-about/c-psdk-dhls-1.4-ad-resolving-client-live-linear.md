---
description: 对于实时／线性内容，TVSDK将主流内容的块替换为相同持续时间的广告中断，以便时间轴持续时间保持不变。
seo-description: 对于实时／线性内容，TVSDK将主流内容的块替换为相同持续时间的广告中断，以便时间轴持续时间保持不变。
seo-title: 实时／线性广告解析和插入
title: 实时／线性广告解析和插入
uuid: 69f287aa-b707-442b-8e07-16f81b242c4b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 实时／线性广告解析和插入{#live-linear-ad-resolving-and-insertion}

对于实时／线性内容，TVSDK将主流内容的块替换为相同持续时间的广告中断，以便时间轴持续时间保持不变。

在播放之前和播放过程中，TVSDK会解析已知广告，用相同持续时间的广告中断替换部分主内容，并在必要时重新计算虚拟时间轴。 广告中断的位置由清单定义的提示点指定。

TVSDK通过以下方式插入广告：

* **预卷**，即内容的开头。
* **中间**，它位于内容中间。

即使持续时间比提示点替换持续时间长或短，TVSDK也接受广告中断。 默认情况下，TVSDK在解析和 `#EXT-X-CUE` 置入广告时支持将提示作为有效的广告标记。 此标记需要以秒为单 `DURATION` 位的元数据字段和提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>在实施习 `AdPolicySelector`惯时，可以对中的预卷、中卷和后卷给出不同的策略， `AdBreakTimelineItem`这 `AdPolicyInfo`些策略基于s的类型 `AdBreakTimelineItem`。例如，您可以在播放中间卷内容后保留该内容，但在播放后删除前卷内容。

播放开始后，视频引擎会定期刷新清单文件。 TVSDK解析任何新广告，并在清单中定义的实时流或线性流中遇到提示点时插入广告。 在解析和插入广告后，TVSDK再次计算虚拟时间轴并调度事 `TimelineEvent.TIMELINE_UPDATED` 件。
