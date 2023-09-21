---
title: 颁发绑定域的许可证
description: 颁发绑定域的许可证
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 颁发绑定域的许可证{#issuing-domain-bound-licenses}

为了使用需要域注册的策略颁发许可证，客户端请求必须包括策略中指定的域服务器颁发的有效域令牌。 当客户端请求许可证时，如果它已经向内容元数据中指定的任何域服务器注册，它将自动包含这些域服务器的域令牌。 如果所选策略需要域注册，SDK将从请求中自动选择域令牌以将许可证绑定到，如果未找到相应的域令牌，则会返回错误。

如果域令牌未过期并且是由授权的域CA颁发的，则被视为有效。 许可证服务器必须通过配置来指定接受域令牌的域颁发机构 `HandlerConfiguration.setDomainCAs()`. 如果未配置域CA，则许可证服务器将无法颁发绑定域的许可证。

如果元数据包括多个策略，则许可证服务器业务逻辑可以根据客户端是否提供域令牌来选择策略。 使用 `LicenseRequestMessage.getDomainTokens()` 确定客户端已注册的域。
