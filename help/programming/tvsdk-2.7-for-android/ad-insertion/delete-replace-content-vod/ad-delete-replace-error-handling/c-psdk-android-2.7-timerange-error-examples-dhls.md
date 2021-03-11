---
description: TVSDK通过合并或替换适当的时间范围来响应错误的时间范围规范。
title: 时间范围错误示例
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# 时间范围错误示例{#time-range-error-examples}

TVSDK通过合并或替换适当的时间范围来响应错误的时间范围规范。

**DELETE时间范围**

在下面的示例中，定义了四个相交的DELETE时间范围。 TVSDK将四个时间范围合并为一个，因此实际删除范围是0到50秒。

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

**REPLACE时间范围**

在下面的示例中，四个REPLACE时间范围被定义为冲突的时间范围。 在这种情况下，TVSDK用25个广告替换0到50个。 它按排序顺序与第一个替换持续时间相同，因为后续范围中存在冲突。

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

