---
title: 处理同步请求
description: 处理同步请求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 处理同步请求 {#handle-synchronization-requests}

如果许可证指定同步要求  [同步要求，](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) 客户端基于在许可证中指定的频率定期向服务器发送同步请求。 要启用同步消息，请设置 `SyncFrequencyRequirements` 在PlayRight。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 如果客户端和服务器都支持协议版本5，则请求URL为“License Server URL in metadata： + ” [!DNL /flashaccess/sync/v4]“。 否则，请求URL为“元数据中的许可证服务器URL”+ &quot; [!DNL /flashaccess/sync/v3]&quot;

同步消息用于将客户端的时间与服务器的时间同步。 如果许可证嵌入在内容中并且不需要从许可证服务器中检索，则同步客户端的时间对于防止客户端修改其时钟以绕过许可证过期很重要。

同步消息还可用于将客户端状态信息传递给服务器( `getClientState()`)进行回滚检测。

请参阅 [回滚保护](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection).
