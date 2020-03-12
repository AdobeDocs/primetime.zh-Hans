---
description: 对于实时／线性内容，TVSDK将主流内容的块替换为相同持续时间的广告中断，以便时间轴持续时间保持不变。
seo-description: 对于实时／线性内容，TVSDK将主流内容的块替换为相同持续时间的广告中断，以便时间轴持续时间保持不变。
seo-title: 实时／线性广告解析和插入
title: 实时／线性广告解析和插入
uuid: a63c97c3-00c5-4dee-a42c-30b70e432b93
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 实时／线性广告解析和插入 {#live-linear-ad-resolving-and-insertion}

对于实时／线性内容，TVSDK将主流内容的块替换为相同持续时间的广告中断，以便时间轴持续时间保持不变。

在播放之前和播放过程中，TVSDK会解析已知广告，用相同持续时间的广告中断替换部分主内容，并在必要时重新计算虚拟时间轴。 广告中断的位置由清单定义的提示点指定。

TVSDK通过以下方式插入广告：

* **在内容的开头**，预先滚动。
* **中间**，在内容中间。

即使持续时间比提示点替换持续时间长或短，TVSDK也接受广告中断。 默认情况下，TVSDK在解析和 `#EXT-X-CUE` 置入广告时支持将提示作为有效的广告标记。 此标记需要以秒为单 `DURATION` 位的元数据字段和提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定义并订阅其他提示（标记）。

播放开始后，视频引擎会定期刷新清单文件。 TVSDK解析任何新广告，并在清单中定义的实时流或线性流中遇到提示点时插入广告。 在解析和插入广告后，TVSDK再次计算虚拟时间轴并调度事 `TimelineItemsUpdatedEventListener.onTimelineUpdated` 件。
