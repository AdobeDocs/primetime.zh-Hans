---
description: 为了照顾那些希望只支付其使用费用而不是固定费用（无论实际使用如何）的客户，Adobe会收集使用情况指标并使用这些指标确定向客户收取的费用。
seo-description: 为了照顾那些希望只支付其使用费用而不是固定费用（无论实际使用如何）的客户，Adobe会收集使用情况指标并使用这些指标确定向客户收取的费用。
seo-title: 计费指标
title: 计费指标
uuid: 6ae9eb1e-4b03-467f-b80a-96313bd01543
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 计费指标 {#billing-metrics}

为了照顾那些希望只支付其使用费用而不是固定费用（无论实际使用如何）的客户，Adobe会收集使用情况指标并使用这些指标确定向客户收取的费用。

每当播放器生成流启动事件时，TVSDK就会开始定期向Adobe的计费系统发送HTTP消息。 对于标准VOD、专业VOD（启用中间广告）和实时内容，期间（称为可计费持续时间）可以不同。 每种内容类型的默认持续时间为30分钟，但您与Adobe的合同将决定实际值。

消息包含以下信息：

* 内容类型（实时、线性或VOD）
* 内容URL
* 是否启用广告
* 是否启用中间广告（仅限VOD）
* 流是否受DRM保护
* TVSDK版本和平台

Adobe预先配置此安排，但您可以与Adobe Enablement代表一起更改安排，与Adobe Enablement代表合作。

要监视TVSDK发送给Adobe的统计信息，请从您的Adobe Enablement Presentative获得URL，然后使用网络捕获工具（如Charles）查看数据。