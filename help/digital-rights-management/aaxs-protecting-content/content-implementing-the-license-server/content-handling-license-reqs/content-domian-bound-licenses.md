---
title: 颁发绑定域的许可证
description: 颁发绑定域的许可证
copied-description: true
exl-id: b9823ae4-d88f-4580-a2ce-275ed3e32f51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 颁发绑定域的许可证{#issuing-domain-bound-licenses}

要使用需要域注册的策略颁发许可证，客户端请求必须包含策略中指定的域服务器颁发的有效域令牌。 当客户端请求许可证时，如果它已向内容元数据中指定的任何域服务器注册，它将自动包含这些域服务器的域令牌。 如果所选策略需要域注册，SDK将从请求中自动选择域令牌以将许可证绑定到，如果未找到合适的域令牌，则会返回错误。

如果域令牌未过期并且是由授权的域CA颁发的，则被视为有效。 许可证服务器必须通过配置来指定接受域令牌的域颁发机构 `HandlerConfiguration.setDomainCAs()`. 如果未配置域CA，则许可证服务器将无法颁发绑定域的许可证。

如果元数据包括多个策略，则许可证服务器业务逻辑可以根据客户端是否提供域令牌来选择策略。 使用 `LicenseRequestMessage.getDomainTokens()` 确定客户端已注册的域。
