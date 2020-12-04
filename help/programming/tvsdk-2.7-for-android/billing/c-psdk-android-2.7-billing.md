---
description: 为了迎合那些希望只支付其使用费用而不是固定费用的客户，Adobe会收集使用情况指标并使用这些指标来确定向客户收取的费用。
seo-description: 为了迎合那些希望只支付其使用费用而不是固定费用的客户，Adobe会收集使用情况指标并使用这些指标来确定向客户收取的费用。
seo-title: 计费指标
title: 计费指标
uuid: 4a03995a-60f6-440e-9cdf-9c0b9c5f1d90
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 概述{#billing-metrics-overview}

为了迎合那些希望只支付其使用费用而不是固定费用的客户，Adobe会收集使用情况指标并使用这些指标来确定向客户收取的费用。

每次播放器生成流开始事件时，TVSDK开始会定期向Adobe的计费系统发送HTTP消息。 对于标准VOD、专业VOD（启用中间广告）和实时内容，期间（称为付费持续时间）可以不同。 每种内容类型的默认持续时间为30分钟，但您与Adobe的合同将决定实际值。

这些消息包含以下信息：

* 内容类型（实时、线性或VOD）
* 内容URL
* 是否启用广告
* 是否启用中间广告（仅限VOD）
* 流是否受DRM保护
* TVSDK版本和平台

Adobe预先配置此安排，但您可以与Adobe支持代表一起更改安排，与Adobe支持代表合作。

要监视TVSDK发送给Adobe的统计信息，请从Adobe支持代表处获取URL，然后使用网络捕获工具（如Charles）查看数据。
