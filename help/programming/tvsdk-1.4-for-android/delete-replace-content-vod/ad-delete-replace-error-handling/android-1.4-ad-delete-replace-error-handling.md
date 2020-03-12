---
description: TVSDK会根据特定问题处理时间范围错误，即合并或重新排序不正确定义的时间范围。
seo-description: TVSDK会根据特定问题处理时间范围错误，即合并或重新排序不正确定义的时间范围。
seo-title: 广告删除和替换错误处理
title: 广告删除和替换错误处理
uuid: e2e06f13-9813-4d86-b6fe-3d09f3bdb100
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 广告删除和替换错误处理{#ad-deletion-and-replacement-error-handling}

TVSDK会根据特定问题处理时间范围错误，即合并或重新排序不正确定义的时间范围。

TVSDK通过执行默 `timeRanges` 认合并和重新排序处理错误。 首先，它按开始时间对客户定义的时间范围 *进行排序* 。 根据这种排序顺序，它然后合并相邻的范围，并且如果范围之间有子集和交集，则将其连接。

TVSDK处理时间范围错误，如下所示：

* 无序- TVSDK会重新排序时间范围。
* 子集- TVSDK将合并时间范围子集。
* 交集- TVSDK将合并交叉的时间范围。
* 替换范围冲突- TVSDK从冲突组中出现的最早时间选择 `timeRange` 替换持续时间。

TVSDK处理与广告元数据的信令模式冲突，如下所示：

* 如果广告信令模式与时间范围元数据冲突，则时间范围元数据始终具有优先级。 例如，如果广告信令模式设置为服务器映射或清单提示，并且广告元数据中也有MARK时间范围，则产生的行为是标记这些范围，而不插入任何广告。
* 对于REPLACE范围，如果信令模式设置为服务器映射或清单提示，则根据REPLACE范围中的指定替换这些范围，并且不会通过服务器映射或清单提示插入广告。 请参阅 [广告信令模式](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md)。

当服务器不返回有效时 `AdBreaks`:

* TVSDK生成并处 `NOPTimelineOperation` 理空的 `AdBreak`。 不播放广告。

对于实时流的时间范围：

* 尽管此C3广告删除／替换功能仅针对VOD提供支持，但实时流的时间范围也会得到处理（如果在广告元数据中指定）。

## 时间范围错误示例 {#time-range-error-examples}

TVSDK会根据需要合并或替换时间范围，以响应错误的时间范围规范。

在以下示例中，定义了四个交叉的DELETE时间范围。 TVSDK将四个时间范围合并为一个时间范围，因此实际删除范围是0到50秒。

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

在以下示例中，四个REPLACE时间范围被定义为冲突的时间范围。 在这种情况下，TVSDK用25个广告替换0到50个广告。 它按排序顺序与第一个替换持续时间相同，因为后续范围内存在冲突。

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
