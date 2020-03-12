---
seo-title: 自定义身份验证／授权概述（可选）
title: 自定义身份验证／授权概述（可选）
uuid: 8b5e38a5-562c-4781-ac40-4b3d6cdd97fe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 自定义身份验证／授权概述（可选）{#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM可配置为连接到您自己的后端身份验证／授权服务以确定：

* 此用户是否可以获得许可证？
* 许可证应包含哪些权利／限制？

Primetime Cloud DRM包括后端身份验证／授权服务的参考实现。 为了演示目的，此服务器对BEES请求发出“允许”响应。 请参 [!DNL BEESServlet.java] 阅修改服务器行为。

>[!NOTE]
>
>以前，这是一个名为 *Back End Entitlement Server* (BEES)的单独产品，因此在整个文档和源文件中对BEES的引用。

