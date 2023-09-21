---
description: TVSDK根据特定问题处理时间范围错误，包括合并或重新排序不正确定义的时间范围。
title: 广告删除和替换错误处理
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 广告删除和替换错误处理{#ad-deletion-and-replacement-error-handling}

TVSDK根据特定问题处理时间范围错误，包括合并或重新排序不正确定义的时间范围。

TVSDK处理 `timeRanges` 进行默认合并和重新排序时出错。 首先，它根据 *开始* 时间。 然后，它根据此排序顺序合并相邻范围，并在这些范围之间存在子集和交集时连接它们。

TVSDK按以下方式处理时间范围错误：

* 混乱 — TVSDK对时间范围进行重新排序。
* 子集 — TVSDK合并时间范围子集。
* Intersect - TVSDK可合并相交的时间范围。
* 替换范围冲突 — TVSDK从最早出现的持续时间中选择替换持续时间 `timeRange` 在冲突组中。

TVSDK可按如下方式处理信令模式与广告元数据的冲突：

* 如果广告信令模式与时间范围元数据冲突，则时间范围元数据始终具有优先级。 例如，如果广告信令模式设置为服务器映射或清单提示，并且广告元数据中还有MARK时间范围，则产生的行为是标记时间范围，并且不插入广告。
* 对于REPLACE范围，如果将信令模式设置为服务器映射或清单提示，则将按照REPLACE范围中指定的方式替换范围，并且不会通过服务器映射或清单提示插入广告。 请参阅 [广告信令模式](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

当服务器未返回有效值时 `AdBreaks`：

* TVSDK生成并处理 `NOPTimelineOperation` 表示空 `AdBreak`. 无广告播放。

对于包含实时流的时间范围：

* 虽然此C3广告删除/替换功能仅支持VOD，但也会为实时流处理时间范围（如果在广告元数据中指定）。

## 时间范围错误示例 {#time-range-error-examples}

TVSDK通过根据需要合并或替换时间范围来响应错误的时间范围规范。

在以下示例中，定义了四个交叉的DELETE时间范围。 TVSDK将四个时间范围合并为一个，以便实际删除范围是0到50秒。

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000
    }, {
        "begin": 20000,
        "end": 50000
    }, {
        "begin": 0,
        "end": 30000
    }, {
        "begin": 30000,
        "end": 40000
    } ]
}
```

在下面的示例中，四个REPLACE时间范围被定义为具有冲突的时间范围。 在这种情况下，TVSDK会将0-50替换为25个广告。 它适用于按排序顺序排列的第一个替换持续时间，因为后续范围中存在冲突。

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000,
        "replace-duration": 15000
    }, {
        "begin": 20000,
        "end": 50000,
        "replace-duration": 20000
    }, {
        "begin": 0,
        "end": 30000,
        "replace-duration": 25000
    }, {
        "begin": 30000,
        "end": 40000,
        "replace-duration": 30000
    } ]
}
```
