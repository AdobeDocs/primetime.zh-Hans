---
title: 重播保护
description: 重播保护
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 重播保护{#replay-protection}

重播保护可防止攻击者重播许可证请求消息并可能导致对客户端的拒绝服务(DoS)攻击(A) *拒绝服务* 攻击是指攻击者试图阻止服务的合法用户使用该服务。) 例如，使用rollback计数器的重放攻击可能用于“欺骗”许可证服务器，使其认为DRM客户端正在回滚其状态，从而导致帐户暂停。

要了解有关重播保护的更多信息，请参阅 `AbstractRequestMessage.getMessageId()` 该 *Adobe访问API参考*.
