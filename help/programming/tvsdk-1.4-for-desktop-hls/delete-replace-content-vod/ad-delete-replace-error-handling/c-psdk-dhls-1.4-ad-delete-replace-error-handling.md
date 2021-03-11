---
description: TVSDK根据特定问题处理时间范围错误，合并或重新排序不正确定义的时间范围。
title: 广告删除和替换错误处理
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# 广告删除和替换错误处理{#ad-deletion-and-replacement-error-handling}

TVSDK根据特定问题处理时间范围错误，合并或重新排序不正确定义的时间范围。

TVSDK通过执行默认合并和重新排序处理`timeRanges`错误。 首先，它按&#x200B;*begin*&#x200B;时间对客户定义的时间范围进行排序。 根据这种排序顺序，它合并相邻的范围，如果范围之间有子集和交集，则将它们连接起来。

TVSDK处理时间范围错误，如下所示：

* 无序 — TVSDK重新排序时间范围。
* 子集 — TVSDK合并时间范围子集。
* 交集 — TVSDK将合并相交的时间范围。
* 替换范围冲突 — TVSDK从冲突组中最早出现的`timeRange`中选择替换持续时间。

TVSDK处理信令模式冲突，如下所示：

* 如果定义了REPLACE范围，TVSDK会自动将信令模式更改为CUSTOM_RANGE。
* 如果定义了DELETE范围或MARK范围，并且信令模式为CUSTOM_RANGE，则TVSDK将删除或标记这些范围。 此情况下不会插入广告。
* 如果DELETE范围或MARK范围定义替换持续时间，TVSDK将忽略此持续时间。

当服务器未返回有效的`AdBreaks`时：

* TVSDK为空`AdBreak`生成并处理`NOPTimelineOperation`。 无广告播放。

## 时间范围错误示例{#time-range-error-examples}

TVSDK通过合并或替换适当的时间范围来响应错误的时间范围规范。

在下面的示例中，定义了四个相交的DELETE时间范围。 TVSDK将四个时间范围合并为一个，因此实际删除范围是0到50秒。

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

在下面的示例中，四个REPLACE时间范围被定义为冲突的时间范围。 在这种情况下，TVSDK用25个广告替换0到50个。 它按排序顺序与第一个替换持续时间相同，因为后续范围中存在冲突。

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
