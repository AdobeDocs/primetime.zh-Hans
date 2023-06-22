---
description: 参考实施说明了如何为广告设置播放器，包括为广告插入设置视频元数据，并将前置广告、中置广告和后置广告解析为VOD或实时/线性视频流。 它还说明了如何处理可点击的广告。
title: 广告插入
exl-id: 3c2d8fca-2a0e-4577-81f3-7b390f6396e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 广告插入 {#ad-insertion}

参考实施说明了如何为广告设置播放器，包括为广告插入设置视频元数据，并将前置广告、中置广告和后置广告解析为VOD或实时/线性视频流。 它还说明了如何处理可点击的广告。

设置用于广告插入的播放器的过程包括：

* **输入馈送：** 使用广告元数据填充输入馈送。 参见 [目录格式](../set-up-dev-environment/exploring-code/catalog-format.md).
* **参考实施信息源适配器：** 正在分析输入馈送以填充广告元数据对象。
* **广告管理器：** 使用AdsManager检索广告元数据并创建相应的AdProvider。
