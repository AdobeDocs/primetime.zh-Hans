---
title: 印前检查功能，如何启用、排除故障或确定问题
description: 印前检查功能，如何启用、排除故障或确定问题
exl-id: 9e4ec343-371f-4116-915f-191e5f42cb47
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# 预检功能：如何启用、排除故障或确定问题 {#preflight-feature}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

Adobe Primetime身份验证计算preAuthorizeResources的方式已更改。 PreAuthorization API具有新的实施。 此实施取代了仅包含进行多个授权调用的旧解决方案。
PreAuthorization API的外部接口保持不变，程序员应用程序不需要更新。

有三种方式可以计算预检资源：

* **MVPD的分叉连接方法**：这涉及Adobe向MVPD发出多个授权调用（客户端仍必须发出一个预检调用）。
* **渠道排列**：MVPD在SAML身份验证响应中公开登录用户的渠道行，并且Adobe根据该行返回授权的资源。 SAML跟踪器中的SAML authN响应应公开该列表。
* **多渠道授权**：客户端和Adobe身份验证均对一组资源的MVPD进行单个调用。

不论MVPD如何，客户端应用程序都将对Preflight端点(checkPreauthorizedResources API)进行单个调用，从而传递一组资源ID。 根据MVPD支持的上述方法之一，Adobe将返回预授权的资源ID。

如果Preflight基于分支和连接方法，则Adobe Primetime身份验证后端会检查其配置中为“最大预授权调用”设置的值。 这由Adobe配置。

“最大预授权调用”配置的默认值为“5”，这意味着最多只能为分支和连接MVPD在Preflight中发送5个资源。 传递超过5个资源会导致异常，并返回空列表。 这是预期行为。 如果MVPD不支持通道排列或多通道授权，我们可以将此配置为任意值，但只有在将它们咨询为多个分支和连接授权调用后，才会增加其加载时间。

因此，在启用/排除MVPD的预检故障时，需要注意以下事项：

* MVPD支持的方法（分支和联接、通道排队或多通道）。
* 如果仅支持分支和联接，则需要询问程序员将在Preflight调用中发送多少资源ID。
* 需要咨询MVPD，并需要了解发出“n”个分支和连接授权调用的影响。 之后，如果该值大于5，则必须在config中对其进行配置。

**限制**

请注意，对于某些MVPD（如AT&amp;T和TWC），如果其中任何resourceID是在预检调用中发送的resourceID列表中的伪ID或无法识别的ID，则我们不会从Preflight调用中获取任何resourceID，即使我们在该列表中也具有有效且经过授权的资源。
