---
description: TVSDK通过合并或替换适当的时间范围来响应错误的时间范围规范。
title: 时间范围错误示例
exl-id: bf634623-8770-4090-96d7-8facdf4cfc42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 时间范围错误示例 {#time-range-error-examples}

TVSDK通过合并或替换适当的时间范围来响应错误的时间范围规范。

**DELETE时间范围**

在以下示例中，定义了四个相交的DELETE时间范围。 TVSDK将四个时间范围合并为一个，以便实际删除范围是0到50秒。

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

在以下示例中，四个REPLACE时间范围定义为具有冲突的时间范围。 在这种情况下，TVSDK会将0-50替换为25个广告。 它随排序顺序中的第一个替换持续时间一起出现，因为后续范围中存在冲突。

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
