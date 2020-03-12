---
seo-title: 发布域绑定许可证
title: 发布域绑定许可证
uuid: 706650b7-6044-4c01-9f5a-90779127c9e1
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 发布域绑定许可证{#issuing-domain-bound-licenses}

要使用需要域注册的DRM策略发布许可证，客户端的请求必须包括由策略中指定的域服务器发布的有效域令牌。 当客户端请求许可证时，它会自动为在内容元数据中指定的任何域服务器包括其域令牌，前提是它已向这些域服务器注册。 如果选定的DRM策略需要域注册，则SDK随后会从请求中自动选择域令牌，以将许可证绑定到该域令牌，或在未找到相应的域令牌时返回错误。

如果域令牌未过期，并且是由授权域CA发布的，则域令牌被视为有效。 许可证服务器必须指定域授权，然后通过配置接受域令牌 `HandlerConfiguration.setDomainCAs()`。 如果未配置域CA，则许可证服务器将无法发行域绑定许可证。

如果元数据包括多个DRM策略，则许可证服务器业务逻辑可以基于客户端是否提供域令牌来选择DRM策略。 您可以使 `LicenseRequestMessage.getDomainTokens()` 用来确定客户端已注册的域。
