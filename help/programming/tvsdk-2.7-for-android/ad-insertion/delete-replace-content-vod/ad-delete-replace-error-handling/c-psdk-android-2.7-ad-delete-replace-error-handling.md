---
description: TVSDK通过合并或重新排列不正确定义的时间范围，根据特定问题处理时间范围错误。
seo-description: TVSDK通过合并或重新排列不正确定义的时间范围，根据特定问题处理时间范围错误。
seo-title: 广告删除和替换错误处理
title: 广告删除和替换错误处理
uuid: 9a951bc4-b372-4655-8510-3f474171415d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# 概述{#ad-deletion-and-replacement-error-handling-overview}

TVSDK通过合并或重新排列不正确定义的时间范围，根据特定问题处理时间范围错误。

TVSDK通过默认合并和重新排序进程来管理`timeRanges`错误。 首先，播放器按&#x200B;*开始*&#x200B;时间对客户定义的时间范围进行排序。 根据此排序顺序，如果区域之间有子集和交集，TVSDK会合并相邻区域并连接这些区域。

TVSDK使用以下选项处理时间范围错误：

* **无序** 的TVSDK重新排序时间范围。

* **子集** TVSDK合并时间范围子集。

* **IntersectTVSDK** 将合并相交的时间范围。

* **替换范围冲** 突TVSDK从冲突组中显示的最 `timeRange` 早时间选择替换持续时间。

TVSDK通过以下方式处理与广告元数据的信令模式冲突：

* 如果广告信号模式与时间范围元数据冲突，则时间范围元数据始终具有优先级。

   例如，如果广告信号模式设置为服务器映射或清单提示，并且广告元数据中还有MARK时间范围，则产生的行为是标记这些范围，并且不插入任何广告。
* 对于REPLACE范围，如果信令模式被设置为服务器映射或清单提示，则将按照REPLACE范围中的指定替换这些范围，并且不会通过服务器映射或清单提示插入广告。

   有关详细信息，请参阅[对广告插入和从广告信令模式删除的影响中的&#x200B;*信令模式／元数据组合行为*&#x200B;表。](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android)。

请记住以下事项：

* 当服务器未返回有效的`AdBreaks`时，TVSDK为空AdBreak生成并处理`NOPTimelineOperation`，并且不播放广告。

* 尽管C3广告删除／替换只针对VOD提供支持，但如果在广告元数据中指定，实时流也会处理时间范围。

