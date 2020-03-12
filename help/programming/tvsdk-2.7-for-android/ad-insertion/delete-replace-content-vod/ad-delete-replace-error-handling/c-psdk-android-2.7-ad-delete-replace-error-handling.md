---
description: TVSDK通过合并或重新排序不正确定义的时间范围，根据特定问题处理时间范围错误。
seo-description: TVSDK通过合并或重新排序不正确定义的时间范围，根据特定问题处理时间范围错误。
seo-title: 广告删除和替换错误处理
title: 广告删除和替换错误处理
uuid: 9a951bc4-b372-4655-8510-3f474171415d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# 概述 {#ad-deletion-and-replacement-error-handling-overview}

TVSDK通过合并或重新排序不正确定义的时间范围，根据特定问题处理时间范围错误。

TVSDK通过默 `timeRanges` 认合并和重新排序进程来管理错误。 首先，玩家按开始时间对客户定义的时间范围 *进行排序* 。 根据此排序顺序，如果范围之间有子集和交集，则TVSDK会合并相邻的范围并连接这些范围。

TVSDK通过以下选项处理时间范围错误：

* **无序** TVSDK会重新排序时间范围。

* **子集** TVSDK将合并时间范围子集。

* **Intersect** TVSDK将合并交叉的时间范围。

* **替换范围冲突** ,TVSDK从冲突组中出现的最早 `timeRange` 时间选择替换持续时间。

TVSDK通过以下方式处理与广告元数据的信令模式冲突：

* 如果广告信令模式与时间范围元数据冲突，则时间范围元数据始终具有优先级。

   例如，如果广告信令模式设置为服务器映射或清单提示，并且广告元数据中也有MARK时间范围，则产生的行为是标记这些范围，而不插入任何广告。
* 对于REPLACE范围，如果信令模式设置为服务器映射或清单提示，则根据REPLACE范围中的指定替换这些范围，并且不会通过服务器映射或清单提示插入广告。

   有关详细信息，请参 *阅Effect中的Signalling Mode / Metadata Combination Behaviors* （信令模式／元数据组合行为） [表，该表用于广告插入和从广告信令模式删除……](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

请记住以下事项：

* 当服务器不返回有效时， `AdBreaks`TVSDK会为空AdBreak生成并处 `NOPTimelineOperation` 理一个，并且不会播放任何广告。

* 尽管C3广告删除／替换仅针对VOD，但如果在广告元数据中指定，则实时流的时间范围也会得到处理。

