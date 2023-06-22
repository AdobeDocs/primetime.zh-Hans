---
title: 重播保护
description: 重播保护
copied-description: true
exl-id: 1e6ad730-b150-4e8f-9e79-e6b4fe006bf8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 重播保护{#replay-protection}

重播保护可防止攻击者重播许可证请求消息并可能导致对客户端的拒绝服务(DoS)攻击(A) *拒绝服务* 攻击是指攻击者试图阻止服务的合法用户使用该服务。) 例如，使用回滚计数器的重播攻击可能用于“欺骗”许可证服务器，使其认为DRM客户端正在回滚其状态，从而导致帐户暂停。

要了解有关重播保护的更多信息，请参阅 `AbstractRequestMessage.getMessageId()` 此 *Adobe访问API参考*.
