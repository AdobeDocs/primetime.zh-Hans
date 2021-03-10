---
description: 对于实时/线性内容，TVSDK用相同持续时间的广告中断替换主流内容的块，以便时间轴持续时间保持不变。
title: 解析和插入实时/线性广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 解析并插入实时/线性广告{#resolve-and-insert-live-linear-ad}

对于实时/线性内容，TVSDK用相同持续时间的广告中断替换主流内容的块，以便时间轴持续时间保持不变。

在播放之前和播放过程中，TVSDK会解析已知广告，用相同持续时间的广告中断替换部分主内容，并在必要时重新计算虚拟时间轴。 广告断点的位置由清单定义的提示点指定。

TVSDK通过以下方式插入广告：

* **前滚**，放在内容之前。
* **中间滚动**，位于内容的中间。

即使持续时间比提示点替换持续时间长或短，TVSDK也接受广告中断。 默认情况下，TVSDK在解析和放置广告时支持将`#EXT-X-CUE`提示作为有效的广告标记。 此标记要求以秒表示元数据字段`DURATION`值，并且提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定义和订阅其他提示（标记）。

播放开始后，视频引擎会定期刷新清单文件。 TVSDK解析任何新广告，并在清单中定义的实时或线性流中遇到提示点时插入广告。 解析并插入广告后，TVSDK再次计算虚拟时间轴并调度`TimelineItemsUpdatedEventListener.onTimelineUpdated`事件。