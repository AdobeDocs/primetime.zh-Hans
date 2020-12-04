---
seo-title: 重放保护
title: 重放保护
uuid: 75f2be65-b2fc-428a-b853-34a4b30960ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 重放保护{#replay-protection}

对于重播保护，通过调用`RequestMessageBase.getMessageId()`检查最近是否看到消息标识符可能比较谨慎。 如果是，则攻击者可能正在尝试重播请求，应拒绝该请求。 为了检测重放尝试，服务器可以存储最近看到的消息id的列表，并根据缓存的列表检查每个传入请求。 要限制消息标识符需要存储的时间，请调用`HandlerConfiguration.setTimestampTolerance()`。 如果设置了此属性，SDK将拒绝任何时间戳超过指定秒数的服务器时间请求。
