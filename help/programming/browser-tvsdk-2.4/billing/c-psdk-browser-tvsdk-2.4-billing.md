---
description: 为了适应那些只想按客户所使用内容支付而不是按固定费率支付而不想实际使用的客户，Adobe会收集使用情况量度，并使用这些量度来确定向客户收取多少费用。
title: 计费量度
exl-id: f4200573-571f-4ed3-be8c-08b72d4f9e0e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 概述 {#billing-metrics-overview}

为了适应那些只想按客户所使用内容支付而不是按固定费率支付而不想实际使用的客户，Adobe会收集使用情况量度，并使用这些量度来确定向客户收取多少费用。

每次播放器生成流启动事件时，Browser TVSDK就会开始定期向Adobe计费系统发送HTTP消息。 该时段（称为可计费持续时间）对于标准VOD、专业VOD（启用了中置广告）和实时内容可能不同。 每种内容类型的默认持续时间为30分钟，但实际值由您的Adobe合同确定。

这些消息包含以下信息：

* 内容类型（实时、线性或VOD）
* 内容URL
* 是否启用广告
* 是否启用中置广告（仅限VOD）
* 流是否受DRM保护
* 浏览器TVSDK版本和平台

Adobe会预配置此安排，但如果要更改该安排，请与您的Adobe启用代表合作。

要监控Browser TVSDK发送到Adobe的统计数据，请从Adobe启用代表处获取URL，然后使用网络捕获工具（例如Charles）查看数据。
