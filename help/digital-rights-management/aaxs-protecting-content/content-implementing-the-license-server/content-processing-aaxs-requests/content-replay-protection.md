---
seo-title: 重放保护
title: 重放保护
uuid: 75f2be65-b2fc-428a-b853-34a4b30960ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 重放保护{#replay-protection}

对于重播保护，检查消息标识符最近是否通过调用被看到可能是审慎的 `RequestMessageBase.getMessageId()`。 如果是，则攻击者可能尝试重播请求，该请求应被拒绝。 为了检测重放尝试，服务器可以存储最近看到的消息ID的列表并针对缓存的列表检查每个传入的请求。 要限制消息标识符需要存储的时间，请调用 `HandlerConfiguration.setTimestampTolerance()`。 如果设置了此属性，SDK将拒绝任何包含时间戳超过服务器时间指定秒数的请求。
