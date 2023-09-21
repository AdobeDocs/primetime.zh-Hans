---
description: TVSDK通过合并或重新排序不正确定义的时间范围，根据具体问题处理时间范围错误。
title: 广告删除和替换错误处理
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 概述 {#ad-deletion-and-replacement-error-handling-overview}

TVSDK通过合并或重新排序不正确定义的时间范围，根据具体问题处理时间范围错误。

TVSDK管理 `timeRanges` 默认合并和重新排序过程时出错。 首先，播放器按以下规则对客户定义的时间范围进行排序： *开始* 时间。 根据此排序顺序，如果范围之间存在子集和交集，则TVSDK将合并相邻范围并连接这些范围。

TVSDK使用以下选项处理时间范围错误：

* **乱序** TVSDK对时间范围进行重新排序。

* **子集** TVSDK合并时间范围子集。

* **Intersect** TVSDK可合并相交的时间范围。

* **替换范围冲突** TVSDK将从最早的替换持续时间中选择替换持续时间 `timeRange` 出现在冲突组中。

TVSDK通过以下方式处理与广告元数据的信令模式冲突：

* 如果广告信令模式与时间范围元数据冲突，则时间范围元数据始终具有优先级。

  例如，如果广告信令模式设置为服务器映射或清单提示，并且广告元数据中还有MARK时间范围，则产生的行为是标记这些范围，并且不插入任何广告。
* 对于REPLACE范围，如果将信令模式设置为服务器映射或清单提示，则将按照REPLACE范围中指定的方式替换这些范围，并且不会通过服务器映射或清单提示插入广告。

  欲了解更多信息，请参见 *信令模式/元数据组合行为* 中的表 [对从广告信令模式插入和删除广告的影响……](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

请记住以下内容：

* 当服务器未返回有效值时 `AdBreaks`， TVSDK生成并处理 `NOPTimelineOperation` 对于空的AdBreak，不播放任何广告。

* 尽管C3广告删除/替换仅支持VOD，但如果已在广告元数据中指定，则也会为实时流处理时间范围。
