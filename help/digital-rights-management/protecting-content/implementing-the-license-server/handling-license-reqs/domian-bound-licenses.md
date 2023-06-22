---
title: 颁发绑定域的许可证
description: 颁发绑定域的许可证
copied-description: true
exl-id: c29e61e5-d05a-4744-9ec8-7508ed814a57
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 颁发绑定域的许可证{#issuing-domain-bound-licenses}

要使用需要域注册的DRM策略颁发许可证，客户端请求必须包括策略中指定的域服务器颁发的有效域令牌。 当客户端请求许可证时，它会自动包含其用于内容元数据中指定的任何域服务器的域令牌，前提是它已向这些域服务器注册。 如果所选的DRM策略需要域注册，则SDK随后会自动从请求中选择一个域令牌以将许可证绑定到，如果未找到合适的域令牌，则会返回错误。

如果域令牌未过期并且是由授权的域CA颁发的，则被视为有效。 许可证服务器必须指定域授权机构，然后它通过配置接受域令牌 `HandlerConfiguration.setDomainCAs()`. 如果未配置域CA，则许可证服务器将无法颁发绑定域的许可证。

如果元数据包括多个DRM策略，则许可证服务器商业逻辑可以基于客户端是否提供域令牌来选择DRM策略。 您可以使用 `LicenseRequestMessage.getDomainTokens()` 确定客户端已注册的域。
