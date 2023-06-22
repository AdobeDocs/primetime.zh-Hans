---
title: 身份验证令牌超时
description: 身份验证令牌超时
copied-description: true
exl-id: ee9c5b2c-6a79-499c-bd60-718e33bc3a9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 身份验证令牌超时{#timeout-for-authentication-tokens}

Adobe访问SDK生成的所有身份验证令牌都有一个保护应用程序安全的超时间隔。 在处理身份验证请求时，使用Adobe访问SDK指定身份验证令牌的过期时间。 过期后，身份验证令牌不再有效，用户必须向许可证服务器重新进行身份验证。

要了解有关身份验证请求的更多信息，请参阅 *Adobe访问API参考*.
