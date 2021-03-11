---
title: 重播保护
description: 重播保护
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 重放保护{#replay-protection}

重放保护可防止攻击者重新播放许可证请求消息，并可能导致对客户端的拒绝服务(DoS)攻击（*denial-of-service*&#x200B;攻击是攻击者试图阻止某个服务的合法用户使用该服务的一种尝试）。 例如，使用回退计数器的重放攻击可用于“诱骗”许可证服务器，使其认为DRM客户端正在回退其状态，从而导致帐户挂起。

要了解有关重放保护的详细信息，请参阅&#x200B;*Adobe访问API参考*。`AbstractRequestMessage.getMessageId()`
