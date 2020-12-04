---
seo-title: 自定义身份验证／授权概述（可选）
title: 自定义身份验证／授权概述（可选）
uuid: 8b5e38a5-562c-4781-ac40-4b3d6cdd97fe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# 自定义身份验证／授权概述（可选）{#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM可配置为联系您自己的后端身份验证／授权服务，以确定：

* 是否允许此用户获取许可证？
* 许可证应包含哪些权利／限制？

Primetime Cloud DRM包括后端身份验证／授权服务的参考实施。 为了演示目的，此服务器正在发出对BEES请求的“允许”响应。 请参阅[!DNL BEESServlet.java]以修改服务器行为。

>[!NOTE]
>
>以前，这是名为&#x200B;*后端授权服务器*(BEES)的单独产品，因此在此文档和源文件中对BEES的引用。

