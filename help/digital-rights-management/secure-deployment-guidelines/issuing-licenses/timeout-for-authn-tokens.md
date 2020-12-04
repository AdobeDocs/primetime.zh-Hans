---
description: 由Adobe PrimetimeDRM SDK生成的所有身份验证令牌都有一个超时时间间隔，以保护应用程序安全。
seo-description: 由Adobe PrimetimeDRM SDK生成的所有身份验证令牌都有一个超时时间间隔，以保护应用程序安全。
seo-title: 身份验证令牌超时
title: 身份验证令牌超时
uuid: 2c2b0dad-0979-4d49-b109-2700ceb4d722
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 身份验证令牌超时{#timeout-for-authentication-tokens}

由Adobe PrimetimeDRM SDK生成的所有身份验证令牌都有一个超时时间间隔，以保护应用程序安全。

在处理身份验证请求时，使用Primetime DRM SDK指定身份验证令牌的过期时间。 该令牌过期后，该令牌不再有效，用户必须再次与许可证服务器进行身份验证。

要了解有关身份验证请求的更多信息，请参阅[AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html)。
