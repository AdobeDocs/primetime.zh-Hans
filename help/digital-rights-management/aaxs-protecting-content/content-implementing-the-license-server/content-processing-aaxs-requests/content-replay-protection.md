---
title: 重播保护
description: 重播保护
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# 重播保护{#replay-protection}

对于重放保护，检查最近是否通过调用看到了消息标识符可能比较谨慎 `RequestMessageBase.getMessageId()`. 如果是这样，攻击者可能会尝试重放该请求，但应拒绝该请求。 为了检测重放尝试，服务器可以存储最近查看过的消息ID列表，并根据缓存的列表检查每个传入请求。 要限制需要存储消息标识符的时间，请调用 `HandlerConfiguration.setTimestampTolerance()`. 如果设置了此属性，SDK将拒绝任何带有超过服务器时间指定秒数的时间戳的请求。
