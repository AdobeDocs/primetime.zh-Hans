---
description: 重放保护可防止攻击者重放许可证请求消息并可能对客户端造成拒绝服务(DoS)攻击。
seo-description: 重放保护可防止攻击者重放许可证请求消息并可能对客户端造成拒绝服务(DoS)攻击。
seo-title: 重放保护
title: 重放保护
uuid: 93749dd3-a42c-4866-ac54-1b20d6683c42
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# 重放保护{#replay-protection}

重放保护可防止攻击者重放许可证请求消息并可能对客户端造成拒绝服务(DoS)攻击。

DoS攻击是攻击者试图阻止服务的合法用户使用该服务。 例如，使用回滚计数器的重放攻击可用于“诱骗”许可证服务器，使其认为DRM客户端已回滚其状态，这会导致帐户挂起。

要了解有关重放保护的更多信息，请参阅[ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())。
