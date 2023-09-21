---
description: TVSDK通过根据需要合并或替换时间范围来响应错误的时间范围规范。
title: 时间范围错误示例
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 时间范围错误示例{#time-range-error-examples}

TVSDK通过根据需要合并或替换时间范围来响应错误的时间范围规范。

**DELETE时间范围**

在以下示例中，定义了四个交叉的DELETE时间范围。 TVSDK将四个时间范围合并为一个，以便实际删除范围是0到50秒。

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000
        },
        {
            "begin": 20000,
            "end": 50000
        },
        {
            "begin": 0,
            "end": 30000
        },
        {
            "begin": 30000,
            "end": 40000
        }
    ]
}
```

**替换时间范围**

在下面的示例中，四个REPLACE时间范围被定义为具有冲突的时间范围。 在这种情况下，TVSDK会将0-50替换为25个广告。 它适用于按排序顺序排列的第一个替换持续时间，因为后续范围中存在冲突。

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000,
            "replace-duration": 15000
        },
        {
            "begin": 20000,
            "end": 50000,
            "replace-duration": 20000
        },
        {
            "begin": 0,
            "end": 30000,
            "replace-duration": 25000
        },
        {
            "begin": 30000,
            "end": 40000,
            "replace-duration": 30000
        }
    ]
}
```
