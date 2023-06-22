---
title: 用户身份验证
description: 用户身份验证
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# 用户身份验证 {#user-authentication}

Adobe Primetime DRM请求可以包含身份验证令牌。

如果使用用户名/密码身份验证，请求可能包含 `AuthenticationToken` 生成者 `AuthenticationHandler`. 如果要访问和验证令牌，则需要使用 `RequestMessageBase.getAuthenticationToken()`. 要在客户端上启动用户名/密码请求，请使用 `DRMManager.authenticate()` ActionScript或iOS API。

如果客户端和服务器使用自定义身份验证机制，则客户端通过其他渠道获取身份验证令牌，并使用设置自定义身份验证令牌 `DRMManager.setAuthenticationToken` ActionScript3.0 API。 使用 `RequestMessageBase.getRawAuthenticationToken()` 以获取自定义身份验证令牌。 服务器实施确定自定义身份验证令牌是否有效。
