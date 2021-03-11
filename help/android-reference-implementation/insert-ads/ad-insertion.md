---
description: 该参考实现说明了如何为广告设置播放器，包括为广告插入设置视频元数据并将前、中、后滚动广告解析为VOD或实时/线性视频流。 它还说明了如何处理可点击广告。
title: 广告插入
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 广告插入{#ad-insertion}

该参考实现说明了如何为广告设置播放器，包括为广告插入设置视频元数据并将前、中、后滚动广告解析为VOD或实时/线性视频流。 它还说明了如何处理可点击广告。

为广告插入设置播放器的过程包括：

* **输入源：使** 用广告元数据填充输入源。请参阅[目录格式](../set-up-dev-environment/exploring-code/catalog-format.md)。
* **引用实现源适配器：** 分析输入源以填充广告元数据对象。
* **AdsManager:** 使用AdsManager检索广告元数据并创建相应的AdProvider。