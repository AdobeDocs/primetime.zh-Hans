---
description: com.adobe.mediacore.timeline.TimelineMarker接口现在包含新方法
title: 从2.5.x延迟广告解析升级到3.0.0延迟广告解析（API/工作流更改）
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 从2.5.x延迟广告解析升级到3.x延迟广告解析（API/工作流更改）：{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

com.adobe.mediacore.timeline.TimelineMarker接口现在包含一个新方法：

**Placement.Type getPlacementType()**

此方法将返回投放类型Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL。 如果广告时间未解析， `getDuration()`TimelineMarker界面上的方法将返回0。

>[!NOTE]
>
>如果此界面尚未解析，则它并不总是转换为类型com.mediacore.timeline.advertising.AdBreakTimelineItem。 如果能在 `getDuration()` 时间线标记的方法大于0。

**事件更改：**

`kEventAdResolutionComplete` 现已弃用，并且会在播放器进入“已准备”状态后立即触发。 以前仅侦听此事件以绘制清理栏的应用程序应更改此事件以监听 `kEventTimelineUpdated` 仅限。 解决单个广告时间后，将新建一个 `kEventTimelineUpdated` 将调度事件。
