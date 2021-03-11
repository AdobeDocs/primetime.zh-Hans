---
description: 重放保护可防止攻击者重放许可证请求消息并潜在地对客户端造成拒绝服务(DoS)攻击。
title: 重播保护
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 重放保护{#replay-protection}

重放保护可防止攻击者重放许可证请求消息并潜在地对客户端造成拒绝服务(DoS)攻击。

DoS攻击是攻击者试图阻止某个服务的合法用户使用该服务。 例如，使用回退计数器的重放攻击可用于“诱骗”许可证服务器，以使其认为DRM客户端已回退其状态，从而导致帐户挂起。

要了解有关重放保护的详细信息，请参阅[ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())。
