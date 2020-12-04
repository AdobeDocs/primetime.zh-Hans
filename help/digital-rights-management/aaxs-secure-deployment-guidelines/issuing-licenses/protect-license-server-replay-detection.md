---
seo-title: 重放保护
title: 重放保护
uuid: 5e6488e6-0834-4dcf-bc26-55019f5db320
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 重放保护{#replay-protection}

重放保护可防止攻击者重放许可证请求消息并可能导致对客户端的拒绝服务(DoS)攻击（A *拒绝服务*&#x200B;攻击是攻击者阻止服务的合法用户使用该服务的尝试）。 例如，使用回滚计数器的重放攻击可用于“诱骗”许可证服务器，使其认为DRM客户端正在回滚其状态，从而导致帐户挂起。

要了解有关重放保护的更多信息，请参阅`AbstractRequestMessage.getMessageId()`Adobe访问API参考&#x200B;*。*
