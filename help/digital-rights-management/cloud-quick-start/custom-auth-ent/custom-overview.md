---
title: 自定义身份验证/授权概述（可选）
description: 自定义身份验证/授权概述（可选）
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 自定义身份验证/授权概述（可选）{#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM可以配置为联系您自己的后端身份验证/权利服务，以确定：

* 是否允许此用户获取许可证？
* 许可证中应该包含哪些权限/限制？

Primetime Cloud DRM包括后端身份验证/权利服务的参考实施。 出于演示目的，此服务器将对BEES请求发出“允许”响应。 请参阅 [!DNL BEESServlet.java] 修改服务器行为。

>[!NOTE]
>
>以前，这是一个单独的产品，称为 *后端授权服务器* (BEES)，因此本文档和源文件中对BEES的引用。
