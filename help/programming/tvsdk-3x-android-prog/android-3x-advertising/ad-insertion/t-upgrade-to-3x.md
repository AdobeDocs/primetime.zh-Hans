---
description: 'com.adobe.mediacore.timeline.TimelineMarker界面现在包含新方法 '
seo-description: 'com.adobe.mediacore.timeline.TimelineMarker界面现在包含新方法 '
seo-title: '从2.5.x延迟广告解析升级到3.0.0延迟广告解析（API/工作流更改） '
title: '从2.5.x延迟广告解析升级到3.0.0延迟广告解析（API/工作流更改） '
uuid: 5870ceb4-93a8-4c8b-b716-673396122644
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 从2.5.x延迟广告解析升级到3.x延迟广告解析（API/工作流更改）:{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

com.adobe.mediacore.timeline.TimelineMarker界面现在包含一个新方法：

**Placement.Type getPlacementType()**

此方法将返回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL的放置类型。 如果广告中断未解析，则TimelineMarker `getDuration()`界面上的方法将返回0。

>[!NOTE]
>
>如果尚未解析此界面，则该界面不会始终转换为com.mediacore.timeline.advertising.AdBreakTimelineItem类型。 如果TimelineMarker的方法大 `getDuration()` 于0，则它将能够转储。

**活动更改：**

`kEventAdResolutionComplete` 现在已折旧，并且现在在播放器进入PREPARED状态后立即触发。 以前只侦听此活动以绘制划动栏的应用程序应将其更改为仅侦听该 `kEventTimelineUpdated` 活动。 解决单个广告中断后，将 `kEventTimelineUpdated` 调度新事件。
