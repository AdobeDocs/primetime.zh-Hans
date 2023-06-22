---
description: com.adobe.mediacore.timeline.TimelineMarker界面现在包含新方法
title: 从2.5.x延迟广告解决升级到3.0.0延迟广告解决（API/工作流更改）
exl-id: 403ccb25-99a9-4545-9d17-3b71583bc6d8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 从2.5.x延迟广告解析升级到3.x延迟广告解析（API/工作流更改）：{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

com.adobe.mediacore.timeline.TimelineMarker界面现在包含一个新方法：

**Placement.Type getPlacementType()**

此方法将返回投放类型Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL。 如果广告时间未解析， `getDuration()`timelineMarker界面上的方法将返回0。

>[!NOTE]
>
>如果此界面尚未解析，则它并不总是转换为com.mediacore.timeline.advertising.AdBreakTimelineItem类型。 只要能在 `getDuration()` 时间轴标记的方法大于0。

**事件更改：**

`kEventAdResolutionComplete` 现已弃用，播放器现在进入“已准备”状态后会立即触发。 以前仅侦听此事件以绘制清理栏的应用程序应更改此事件以侦听 `kEventTimelineUpdated` 仅此而已。 解决单个广告时间后，将创建一个新的 `kEventTimelineUpdated` 将调度事件。
