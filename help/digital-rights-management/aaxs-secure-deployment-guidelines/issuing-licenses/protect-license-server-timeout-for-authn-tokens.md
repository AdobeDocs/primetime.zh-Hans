---
title: 身份验证令牌超时
description: 身份验证令牌超时
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# 身份验证令牌超时{#timeout-for-authentication-tokens}

由Adobe Access SDK生成的所有身份验证令牌都有一个超时间隔，以保护应用程序安全。 在处理身份验证请求时，使用Adobe访问SDK指定身份验证令牌的过期时间。 到期后，身份验证令牌将失效，用户必须使用许可证服务器重新进行身份验证。

要了解有关身份验证请求的更多信息，请参阅&#x200B;*Adobe访问API参考*&#x200B;中的AuthenticationHandler。
