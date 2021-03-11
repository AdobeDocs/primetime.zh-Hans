---
title: 处理同步请求
description: 处理同步请求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# 处理同步请求{#handling-synchronization-requests}

. 如果许可证指定同步要求（[同步要求](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)），则客户端将根据许可证中指定的频率定期向服务器发送同步请求。 要启用同步消息，请在PlayRight中设置SyncFrequencyRequirements。

* 请求处理程序类为`com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 请求消息类为`com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 如果客户端和服务器支持协议版本5，则请求URL为“元数据中的许可证服务器URL:+ &quot;/flashaccess/sync/v4&quot;。 否则，请求URL为“元数据中的许可证服务器URL”+“/flashaccess/sync/v3”

同步消息用于同步客户端的时间与服务器的时间。 如果许可证嵌入到内容中，并且不需要从许可证服务器检索，则同步客户端的时间对于防止客户端修改其时钟以绕过许可证过期很重要。

同步消息还可用于将客户端状态信息传送到服务器(`getClientState()`)以进行回滚检测。 请参阅[回滚保护](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md)。