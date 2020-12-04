---
description: 为了迎合那些希望只支付其使用费用而不是固定费用的客户，Adobe会收集使用情况指标并使用这些指标来确定向客户收取的费用。
seo-description: 为了迎合那些希望只支付其使用费用而不是固定费用的客户，Adobe会收集使用情况指标并使用这些指标来确定向客户收取的费用。
seo-title: 计费指标
title: 计费指标
uuid: e09b77b3-89d3-44d6-be4e-e1612fbf89fc
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# 概述{#billing-metrics-overview}

为了迎合那些希望只支付其使用费用而不是固定费用的客户，Adobe会收集使用情况指标并使用这些指标来确定向客户收取的费用。

每次播放器生成流开始事件时，浏览器TVSDK开始会定期向Adobe的计费系统发送HTTP消息。 对于标准VOD、专业VOD（启用中间广告）和实时内容，期间（称为付费持续时间）可以不同。 每种内容类型的默认持续时间为30分钟，但您与Adobe的合同将决定实际值。

这些消息包含以下信息：

* 内容类型（实时、线性或VOD）
* 内容URL
* 是否启用广告
* 是否启用中间广告（仅限VOD）
* 流是否受DRM保护
* 浏览器TVSDK版本和平台

Adobe预配置此安排，但如果要更改该安排，请与Adobe支持代表合作。

要监视浏览器TVSDK发送给Adobe的统计信息，请从Adobe支持代表处获取URL，然后使用网络捕获工具（例如，Charles）查看数据。
