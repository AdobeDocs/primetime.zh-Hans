---
title: 重播保护
description: 重播保护
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 重放保护{#replay-protection}

对于重放保护，通过调用`RequestMessageBase.getMessageId()`检查最近是否看到消息标识符可能比较谨慎。 如果是，则攻击者可能正在尝试重放应被拒绝的请求。 为了检测重放尝试，服务器可以存储最近看到的消息ID的列表，并根据缓存的列表检查每个传入请求。 要限制消息标识符需要存储的时间，请调用`HandlerConfiguration.setTimestampTolerance()`。 如果设置了此属性，SDK将拒绝任何包含时间戳超过指定秒数的服务器时间请求。
