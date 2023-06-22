---
title: 自定义身份验证/权利概述（可选）
description: 自定义身份验证/权利概述（可选）
copied-description: true
exl-id: d92c4246-c772-44da-80b6-4086dfc30ff4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 自定义身份验证/权利概述（可选）{#custom-authentication-entitlement-overview-optional}

可以将Primetime Cloud DRM配置为联系您自己的后端身份验证/权利服务以确定：

* 是否允许此用户获取许可证？
* 许可证中应有哪些权限/限制？

Primetime Cloud DRM包括后端身份验证/权利服务的参考实现。 出于演示目的，此服务器将对BEES请求发出“允许”响应。 参见 [!DNL BEESServlet.java] 修改服务器行为。

>[!NOTE]
>
>以前，这是一个单独的产品，称为 *后端授权服务器* (BEES)，因此本文档和源文件中对BEES的引用。
