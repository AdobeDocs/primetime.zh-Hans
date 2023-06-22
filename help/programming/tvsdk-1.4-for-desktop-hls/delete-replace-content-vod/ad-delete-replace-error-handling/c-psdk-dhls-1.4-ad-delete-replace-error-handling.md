---
description: TVSDK根据特定问题处理时间范围错误，包括合并或重新排序不正确定义的时间范围。
title: 广告删除和替换错误处理
exl-id: 86970989-82e0-4e6f-81fb-beee70870c69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 广告删除和替换错误处理 {#ad-deletion-and-replacement-error-handling}

TVSDK根据特定问题处理时间范围错误，包括合并或重新排序不正确定义的时间范围。

TVSDK处理 `timeRanges` 默认合并和重新排序时出错。 首先，它按客户定义的时间范围排序 *开始* 时间。 然后，根据此排序顺序，它合并相邻范围，如果范围之间存在子集和交集，则合并这些范围。

TVSDK按以下方式处理时间范围错误：

* 混乱 — TVSDK对时间范围进行重新排序。
* 子集 — TVSDK合并时间范围子集。
* 相交 — TVSDK合并相交的时间范围。
* 替换范围冲突 — TVSDK从最早出现的替换持续时间中选择替换持续时间 `timeRange` 在冲突组中。

TVSDK按以下方式处理信令模式冲突：

* 如果定义了REPLACE范围，TVSDK会自动将信令模式更改为CUSTOM_RANGE。
* 如果定义了DELETE范围或MARK范围，并且信令模式为CUSTOM_RANGE ，则TVSDK将删除或标记这些范围。 在这种情况下，没有广告插入。
* 如果DELETE范围或MARK范围定义了替换持续时间，则TVSDK将忽略该持续时间。

当服务器未返回有效值时 `AdBreaks`：

* TVSDK生成并处理 `NOPTimelineOperation` 表示空 `AdBreak`. 无广告播放。

## 时间范围错误示例 {#time-range-error-examples}

TVSDK通过合并或替换适当的时间范围来响应错误的时间范围规范。

在以下示例中，定义了四个相交的DELETE时间范围。 TVSDK将四个时间范围合并为一个，以便实际删除范围是0到50秒。

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

在以下示例中，四个REPLACE时间范围定义为具有冲突的时间范围。 在这种情况下，TVSDK会将0-50替换为25个广告。 它随排序顺序中的第一个替换持续时间一起出现，因为后续范围中存在冲突。

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
