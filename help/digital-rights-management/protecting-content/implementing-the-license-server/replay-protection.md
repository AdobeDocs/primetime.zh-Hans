---
seo-title: 重放保护
title: 重放保护
uuid: c737998a-9c33-48b4-b741-91106697d71f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 重放保护{#replay-protection}

对于重放保护，您可能希望检查最近是否通过调用看到消息标识符 `RequestMessageBase.getMessageId()`。 如果是，则攻击者可能尝试重播请求，该请求应被拒绝。 为了检测重放尝试，服务器可以存储最近看到的消息ID的列表并针对缓存的列表检查每个传入的请求。 要限制消息标识符需要存储的时间，请调用 `HandlerConfiguration.setTimestampTolerance()`。 如果设置了此属性，则SDK会拒绝任何包含时间戳超过服务器时间指定秒数的请求。
