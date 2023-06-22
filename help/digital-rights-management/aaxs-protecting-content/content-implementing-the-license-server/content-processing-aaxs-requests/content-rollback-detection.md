---
title: 回滚检测
description: 回滚检测
copied-description: true
exl-id: 525ae64e-1ade-4661-8403-ee4e42181358
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 回滚检测{#rollback-detection}

对于回滚检测，某些使用规则要求客户端维护用于实施权限的状态信息。 例如，要强制实施播放窗口使用规则，客户端将存储用户首次开始查看内容的日期和时间。 此事件触发播放窗口的启动。 为了安全地强制执行播放窗口，服务器需要确保用户没有备份和恢复客户端状态，以便删除存储在客户端上的播放窗口开始时间。 服务器通过跟踪客户端回滚计数器的值来执行此操作。 对于每个请求，服务器通过调用获取计数器的值 `RequestMessageBase.getClientState()` 以获取 `ClientState` 对象，然后调用 `ClientState.getCounter()` 以获取客户端状态计数器的当前值。 服务器应该为每个客户端存储此值(使用 `MachineId.getUniqueId()` 以标识与回退计数器值关联的客户端)，然后调用 `ClientState.incrementCounter()` 将计数器值增加1。 如果服务器检测到计数器值小于服务器看到的最后一个值，则客户端状态可能已回滚。 有关客户端状态篡改检测的更多信息，请参见 `ClientState` API参考文档。
