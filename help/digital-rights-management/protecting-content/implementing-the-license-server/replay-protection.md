---
title: 重播保护
description: 重播保护
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 重播保护{#replay-protection}

对于重播保护，您可能希望通过调用来检查最近是否看到消息标识符 `RequestMessageBase.getMessageId()`. 如果是这样，攻击者可能会尝试重播该请求，而应拒绝该请求。 为了检测重放尝试，服务器可以存储最近查看的邮件ID列表，并根据缓存列表检查每个传入请求。 要限制需要存储消息标识符的时间，请调用 `HandlerConfiguration.setTimestampTolerance()`. 如果设置了此属性，则SDK会拒绝任何包含时间戳且时间戳超过服务器时间指定秒数的请求。
