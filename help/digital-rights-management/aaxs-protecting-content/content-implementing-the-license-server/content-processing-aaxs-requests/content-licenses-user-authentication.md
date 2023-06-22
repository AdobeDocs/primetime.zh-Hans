---
title: 用户身份验证
description: 用户身份验证
copied-description: true
exl-id: a0dd7d81-2249-4845-94da-53b755d6cd7c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 用户身份验证{#user-authentication}

Adobe访问请求可以包含身份验证令牌。

如果使用用户名/密码身份验证，请求可能包含 `AuthenticationToken` 生成者 `AuthenticationHandler`. 要访问和验证令牌，请使用 `RequestMessageBase.getAuthenticationToken()`. 要在客户端上启动用户名/密码请求，请使用 `DRMManager.authenticate()` ActionScript或iOS API。

如果客户端和服务器使用自定义身份验证机制，则客户端通过其他渠道获取身份验证令牌，并使用设置自定义身份验证令牌 `DRMManager.setAuthenticationToken` ActionScript3.0 API。 使用 `RequestMessageBase.getRawAuthenticationToken()` 以获取自定义身份验证令牌。 服务器实施负责确定自定义身份验证令牌是否有效。
