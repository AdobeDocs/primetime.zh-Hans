---
seo-title: 回滚检测
title: 回滚检测
uuid: cc554194-2848-4104-85eb-f697a86c72f2
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 回滚检测{#rollback-detection}

对于回滚检测，某些使用规则要求客户端维护状态信息以执行权限。 例如，为了实施播放窗口使用规则，客户端存储用户首次开始查看内容的日期和时间。 此事件会触发播放窗口的开始。 为了安全地强制播放窗口，服务器需要确保用户不备份和恢复客户端状态，以删除存储在客户端上的播放窗口开始时间。 服务器通过跟踪客户端的回滚计数器的值来执行此操作。 对于每个请求，服务器通过调用获取对象来获取计数器的值， `RequestMessageBase.getClientState()` 然后调 `ClientState` 用 `ClientState.getCounter()` 来获取客户端状态计数器的当前值。 服务器应为每个客户端存储此值(用于标识与回滚计数器值关联的客户端 `MachineId.getUniqueId()` )，然后调用该值 `ClientState.incrementCounter()` 将计数器值增加1。 如果服务器检测到计数器值小于服务器看到的最后一个值，则客户端状态可能已回滚。 有关客户端状态篡改检测的详细信息，请参阅 `ClientState` API参考文档。
