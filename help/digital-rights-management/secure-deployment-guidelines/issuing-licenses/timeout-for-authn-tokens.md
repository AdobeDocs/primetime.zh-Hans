---
description: Adobe Primetime DRM SDK生成的所有身份验证令牌都有一个保护应用程序安全的超时间隔。
title: 身份验证令牌超时
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 身份验证令牌超时{#timeout-for-authentication-tokens}

Adobe Primetime DRM SDK生成的所有身份验证令牌都有一个保护应用程序安全的超时间隔。

在处理身份验证请求时，使用Primetime DRM SDK指定身份验证令牌的过期时间。 令牌过期后不再有效，用户必须再次通过许可证服务器进行身份验证。

要了解有关身份验证请求的更多信息，请参阅 [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
