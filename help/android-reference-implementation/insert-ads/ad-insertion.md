---
description: 参考实施说明了如何为广告设置播放器，包括为广告插入设置视频元数据，并将前置广告、中置广告和后置广告解析为VOD或实时/线性视频流。 它还说明了如何处理可点击广告。
title: Ad insertion
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Ad insertion {#ad-insertion}

参考实施说明了如何为广告设置播放器，包括为广告插入设置视频元数据，并将前置广告、中置广告和后置广告解析为VOD或实时/线性视频流。 它还说明了如何处理可点击广告。

设置用于广告插入的播放器的过程包括：

* **输入馈送：** 使用广告元数据填充输入馈送。 请参阅 [目录格式](../set-up-dev-environment/exploring-code/catalog-format.md).
* **参考实施信息源适配器：** 正在分析输入馈送以填充广告元数据对象。
* **AdsManager：** 使用AdsManager检索广告元数据并创建相应的AdProvider。
