---
title: 处理同步请求
description: 处理同步请求
copied-description: true
exl-id: b19245e3-19ae-4dd4-9e5e-6956feb91334
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 处理同步请求 {#handle-synchronization-requests}

如果许可证指定同步要求  [同步要求，](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) 客户端基于许可证中指定的频率定期向服务器发送同步请求。 要启用同步消息，请设置 `SyncFrequencyRequirements` 在PlayRight中。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 如果客户端和服务器都支持协议版本5，则请求URL为“元数据中的许可证服务器URL： + ” [!DNL /flashaccess/sync/v4]“。 否则，请求URL为“元数据中的许可证服务器URL”+ &quot; [!DNL /flashaccess/sync/v3]”

同步消息用于将客户端的时间与服务器的时间同步。 如果许可证嵌入在内容中并且不需要从许可证服务器中检索，则同步客户端的时间对于防止客户端修改其时钟以绕过许可证过期很重要。

同步消息还可用于将客户端状态信息传递给服务器( `getClientState()`)进行回滚检测。

参见 [回滚保护](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection).
