---
seo-title: 用户身份验证
title: 用户身份验证
uuid: 5cbd76b9-ff64-4a4b-8cfd-54f05c04eaa3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 用户身份验证 {#user-authentication}

Adobe Primetime DRM请求可包含身份验证令牌。

如果使用用户名／密码身份验证，则请求可能包含由 `AuthenticationToken` 生成的 `AuthenticationHandler`。 如果要访问并验证令牌，您需要使用 `RequestMessageBase.getAuthenticationToken()`。 要在客户端上发起用户名／密码请求，请使 `DRMManager.authenticate()` 用ActionScript或iOS API。

如果客户端和服务器使用自定义身份验证机制，则客户端通过某些其他通道获得身份验证令牌，并使用 `DRMManager.setAuthenticationToken` ActionScript 3.0 API设置自定义身份验证令牌。 使用 `RequestMessageBase.getRawAuthenticationToken()` 获取自定义身份验证令牌。 服务器实现确定自定义身份验证令牌是否有效。
