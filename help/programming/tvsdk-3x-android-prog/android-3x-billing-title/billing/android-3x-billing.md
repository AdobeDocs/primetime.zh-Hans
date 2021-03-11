---
description: 为了照顾那些只想为所用内容而非固定费用付费（无论实际用途如何）的客户，Adobe会收集使用量度并使用这些量度来确定向客户收取多少费用。
title: 账单量度
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# 帐单量度{#billing-metrics}

为了照顾那些只想为所用内容而非固定费用付费（无论实际用途如何）的客户，Adobe会收集使用量度并使用这些量度来确定向客户收取多少费用。

每次播放器生成流开始事件时，TVSDK开始会定期向Adobe的计费系统发送HTTP消息。 对于标准VOD、专业VOD（启用中间广告）和实时内容，期间（称为可计费持续时间）可以不同。 每种内容类型的默认持续时间为30分钟，但您与Adobe的合同将决定实际值。

这些消息包含以下信息：

* 内容类型（实时、线性或VOD）
* 内容URL
* 是否启用广告
* 是否启用中间广告（仅VOD）
* 流是否受DRM保护
* TVSDK版本和平台

Adobe预先配置此安排，但您可以与Adobe支持代表一起更改安排，与Adobe支持代表合作。

要监视TVSDK发送给Adobe的统计信息，请从您的Adobe支持代表处获取URL，并使用网络捕获工具（如Charles）查看数据。