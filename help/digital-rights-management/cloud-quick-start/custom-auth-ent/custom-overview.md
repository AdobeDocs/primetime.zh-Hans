---
title: 自定义身份验证/授权概述（可选）
description: 自定义身份验证/授权概述（可选）
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# 自定义身份验证/授权概述（可选）{#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM可配置为联系您自己的后端身份验证/授权服务，以确定：

* 是否允许此用户获得许可证？
* 许可证应包含哪些权利/限制？

Primetime Cloud DRM包括后端身份验证/授权服务的参考实施。 出于演示目的，此服务器正在对BEES请求发出“允许”响应。 请参阅[!DNL BEESServlet.java]以修改服务器行为。

>[!NOTE]
>
>以前，这是名为&#x200B;*Back End Entitlement Server*(BEES)的单独产品，因此在此文档和源文件中对BEES的引用。

