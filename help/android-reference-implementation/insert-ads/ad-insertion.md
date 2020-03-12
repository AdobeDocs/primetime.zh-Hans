---
description: 该参考实现说明了如何为广告设置播放器，包括为广告插入设置视频元数据并将滚动前、中间和滚动后广告解析到VOD或实时／线性视频流中。 它还说明了如何处理可点击广告。
seo-description: 该参考实现说明了如何为广告设置播放器，包括为广告插入设置视频元数据并将滚动前、中间和滚动后广告解析到VOD或实时／线性视频流中。 它还说明了如何处理可点击广告。
seo-title: 广告插入
title: 广告插入
uuid: 75c1d77a-a7ff-4cb6-ad7f-7c83a950b7cb
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 广告插入 {#ad-insertion}

该参考实现说明了如何为广告设置播放器，包括为广告插入设置视频元数据并将滚动前、中间和滚动后广告解析到VOD或实时／线性视频流中。 它还说明了如何处理可点击广告。

为广告插入设置播放器的过程包括：

* **输入源：** 使用广告元数据填充输入源。 请参阅 [目录格式](../set-up-dev-environment/exploring-code/catalog-format.md)。
* **参考实现源适配器：** 解析输入源以填充广告元数据对象。
* **AdsManager:** 使用AdsManager检索广告元数据并创建相应的AdProvider。