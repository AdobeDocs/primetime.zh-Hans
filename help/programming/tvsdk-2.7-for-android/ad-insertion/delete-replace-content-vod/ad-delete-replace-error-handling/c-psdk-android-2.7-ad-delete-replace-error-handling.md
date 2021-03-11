---
description: TVSDK通过合并或重新排列不正确定义的时间范围，根据特定问题处理时间范围错误。
title: 广告删除和替换错误处理
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 概述{#ad-deletion-and-replacement-error-handling-overview}

TVSDK通过合并或重新排列不正确定义的时间范围，根据特定问题处理时间范围错误。

TVSDK通过默认合并和重新排序进程管理`timeRanges`错误。 首先，播放器按&#x200B;*begin*&#x200B;时间对客户定义的时间范围进行排序。 根据此排序顺序，如果范围之间有子集和交集，TVSDK将合并相邻范围并连接这些范围。

TVSDK可使用以下选项处理时间范围错误：

* **无序** 的TVSDK重新排序时间范围。

* **SubsetTVSDK** 将合并时间范围子集。

* **** IntersectTVSDK将合并相交的时间范围。

* **替换范** 围冲突TVSDK从冲突组中显示 `timeRange` 的最早时间选择替换持续时间。

TVSDK通过以下方式处理与广告元数据的信令模式冲突：

* 如果广告信令模式与时间范围元数据冲突，则时间范围元数据始终具有优先级。

   例如，如果将广告信令模式设置为服务器映射或清单提示，并且广告元数据中还有MARK时间范围，则产生的行为是标记这些范围，而不插入任何广告。
* 对于REPLACE范围，如果信令模式设置为服务器映射或清单提示，则按照REPLACE范围中的指定替换该范围，并且不会通过服务器映射或清单提示插入广告。

   有关详细信息，请参阅[中&#x200B;*信令模式/元数据组合行为*&#x200B;表从广告信令模式插入和删除广告的效果……](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android)。

请记住以下事项：

* 当服务器未返回有效的`AdBreaks`时，TVSDK会为空AdBreak生成并处理`NOPTimelineOperation`，并且不播放任何广告。

* 尽管C3广告删除/替换仅针对VOD受支持，但如果在广告元数据中指定，实时流的时间范围也会得到处理。

