---
description: 'com.adobe.mediacore.timeline.TimelineMarker接口现在包含一种新方法 '
title: '从2.5.x延迟广告解析升级到3.0.0延迟广告解析（API/工作流更改） '
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# 从2.5.x延迟广告解析升级到3.x延迟广告解析（API/工作流更改）：{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

com.adobe.mediacore.timeline.TimelineMarker接口现在包含一种新方法：

**Placement.Type getPlacementType()**

此方法将返回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL的放置类型。 如果广告中断未解析，则TimelineMarker接口上的`getDuration()`方法将返回0。

>[!NOTE]
>
>如果尚未解析此接口，则它不会始终转换为com.mediacore.timeline.advertising.AdBreakTimelineItem类型。 如果TimelineMarker的`getDuration()`方法大于0，则将能够转换它。

**事件更改：**

`kEventAdResolutionComplete` 现在已折旧，并且现在在玩家进入PREPARED状态后立即触发。以前只听取此事件绘制划动栏的应用程序应将其更改为仅侦听`kEventTimelineUpdated`。 解决单个广告中断后，将调度新的`kEventTimelineUpdated`事件。
