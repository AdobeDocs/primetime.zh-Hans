---
seo-title: 处理同步请求
title: 处理同步请求
uuid: 37b2db09-4c09-4216-874b-b570a84569b6
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# 处理同步请求{#handling-synchronization-requests}

. 如果许可证指定了同步要求（[同步要求](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)），则客户端将根据许可证中指定的频率定期向服务器发送同步请求。 要启用同步消息，请在PlayRight中设置SyncFrequencyRequirements。

* 请求处理函数类为`com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 请求消息类为`com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 如果客户端和服务器支持协议版本5，则请求URL为元数据中的“许可证服务器URL:+ &quot;/flashaccess/sync/v4&quot;。 否则，请求URL为“元数据中的许可证服务器URL”+“/flashaccess/sync/v3”

同步消息用于同步客户端的时间与服务器的时间。 如果许可证嵌入到内容中，并且不需要从许可证服务器检索，则同步客户端的时间对于防止客户端修改其时钟以绕过许可证过期很重要。

同步消息还可用于将客户端状态信息传递到服务器(`getClientState()`)以进行回滚检测。 请参阅[回滚保护](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md)。