---
description: 重播保护可防止攻击者重播许可证请求消息并可能导致对客户端的拒绝服务(DoS)攻击。
title: 重播保护
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 重播保护{#replay-protection}

重播保护可防止攻击者重播许可证请求消息并可能导致对客户端的拒绝服务(DoS)攻击。

DoS攻击是攻击者试图阻止服务的合法用户使用该服务的一种尝试。 例如，使用回滚计数器的重播攻击可能用于“诱使”许可证服务器认为DRM客户端已回滚其状态，从而导致帐户挂起。

要了解有关重播保护的更多信息，请参阅 [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).
