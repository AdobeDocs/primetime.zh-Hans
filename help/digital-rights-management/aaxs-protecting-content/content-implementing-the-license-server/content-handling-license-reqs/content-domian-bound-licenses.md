---
title: 发布域范围的许可证
description: 发布域范围的许可证
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 颁发域绑定许可证{#issuing-domain-bound-licenses}

为了使用需要域注册的策略发布许可证，客户端的请求必须包括由策略中指定的域服务器发布的有效域令牌。 当客户端请求许可证时，如果已向这些域服务器注册，则它将自动包括在内容元数据中指定的任何域服务器的域令牌。 如果所选策略需要域注册，则SDK将从请求中自动选择域令牌以将许可证绑定到，或在未找到相应域令牌时返回错误。

如果域令牌未过期，并且是由授权域CA颁发的，则域令牌被视为有效。 许可证服务器必须通过配置`HandlerConfiguration.setDomainCAs()`指定将接受域令牌的域授权。 如果未配置域CA，则许可证服务器将无法颁发域绑定的许可证。

如果元数据包括多个策略，则许可证服务器业务逻辑可以根据客户端是否提供域令牌来选择策略。 使用`LicenseRequestMessage.getDomainTokens()`确定客户端已注册的域。
