---
title: 重播保护
description: 重播保护
copied-description: true
exl-id: dfb6d615-07d2-4303-82cc-10cfee4bb387
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# 重播保护{#replay-protection}

对于重播保护，检查最近是否通过调用看到了消息标识符可能比较谨慎 `RequestMessageBase.getMessageId()`. 如果是这样，攻击者可能会尝试重播该请求，而应拒绝该请求。 为了检测重放尝试，服务器可以存储最近查看的邮件ID列表，并根据缓存列表检查每个传入请求。 要限制需要存储消息标识符的时间，请调用 `HandlerConfiguration.setTimestampTolerance()`. 如果设置了此属性，则SDK将拒绝任何带有超过服务器时间指定秒数的时间戳的请求。
