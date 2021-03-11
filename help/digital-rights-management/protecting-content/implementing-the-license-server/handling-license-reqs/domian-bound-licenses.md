---
title: 颁发域范围的许可证
description: 颁发域范围的许可证
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# 颁发域绑定许可证{#issuing-domain-bound-licenses}

要使用需要域注册的DRM策略颁发许可证，客户端的请求必须包括由策略中指定的域服务器颁发的有效域令牌。 当客户端请求许可证时，它会自动为在内容元数据中指定的任何域服务器包括其域令牌，前提是它已向这些域服务器注册。 如果选定的DRM策略需要域注册，则SDK随后会从请求中自动选择域令牌，以将许可证绑定到或返回错误（如果未找到相应的域令牌）。

如果域令牌未过期，并且是由授权域CA颁发的，则域令牌被视为有效。 许可证服务器必须通过配置`HandlerConfiguration.setDomainCAs()`指定接受域令牌的域授权。 如果未配置域CA，则许可证服务器将无法颁发域绑定的许可证。

如果元数据包括多个DRM策略，则许可证服务器业务逻辑可以基于客户端是否提供域令牌来选择DRM策略。 可以使用`LicenseRequestMessage.getDomainTokens()`确定客户端已注册的域。
