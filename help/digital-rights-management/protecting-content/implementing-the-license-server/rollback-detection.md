---
title: 回滚检测
description: 回滚检测
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# 回滚检测{#rollback-detection}

对于回滚检测，某些使用规则要求客户端维护状态信息以执行权限。 例如，为了实施播放窗口使用规则，客户端存储用户首次开始查看内容的日期和时间。 此事件触发播放窗口的开始。 要安全地强制播放窗口，服务器需要确保用户不备份和恢复客户端状态，以删除存储在客户端上的播放窗口开始时间。 服务器通过跟踪客户端的回滚计数器的值来执行此操作。

对于每个请求，服务器通过调用`RequestMessageBase.getClientState()`获取`ClientState`对象，然后调用`ClientState.getCounter()`获取客户端状态计数器的当前值来获取计数器的值。 服务器应为每个客户端存储此值（使用`MachineId.getUniqueId()`标识与回滚计数器值关联的客户端），然后调用`ClientState.incrementCounter()`将计数器值增加1。 如果服务器检测到计数器值小于服务器看到的最后一个值，则客户端状态可能已回滚。

有关客户端状态篡改检测的详细信息，请参阅`ClientState` API参考文档。
