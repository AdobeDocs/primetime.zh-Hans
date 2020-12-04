---
description: Flash媒体Rights Management服务器1.x和Adobe PrimetimeDRM使用不同的元数据打包内容和请求许可证。 要使Primetime DRM使用FMRMS 1.x版内容，必须转换元数据。
seo-description: Flash媒体Rights Management服务器1.x和Adobe PrimetimeDRM使用不同的元数据打包内容和请求许可证。 要使Primetime DRM使用FMRMS 1.x版内容，必须转换元数据。
seo-title: 确保与Flash媒体Rights Management服务器1.x的兼容性
title: 确保与Flash媒体Rights Management服务器1.x的兼容性
uuid: dd70941e-9015-4fb0-b265-557b6252e051
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# 确保与Flash媒体Rights Management服务器1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}的兼容性

Flash媒体Rights Management服务器1.x和Adobe PrimetimeDRM使用不同的元数据打包内容和请求许可证。 要使Primetime DRM使用FMRMS 1.x版内容，必须转换元数据。

Primetime DRM SDK支持以下元数据转换选项：

* 脱机（推荐）

   在脱机流程中生成Primetime DRM元数据，并存储元数据，直到客户请求它。 如果元数据是脱机生成的，则许可证服务器无需访问1.x CEK或打包程序凭据。 转换脱机优惠的性能更好，因为许可证服务器无需实时生成元数据。
* 按需

   Primetime DRM元数据是在客户请求元数据时生成的。 当Primetime DRM客户端下载版本1.x内容时，客户端将DRM元数据发送到Primetime DRM SDK。 SDK将DRM元数据转换为当前格式，加密内容加密密钥(CEK)并将其嵌入到元数据中，并将内容发送回Primetime DRM客户端。

   >[!NOTE]
   >
   >Primetime DRM 1.x元数据不包括CEK。

   要转换元数据，Primetime DRM需要访问Primetime DRM 1.x内容加密密钥。 从Flash媒体Rights Management服务器1.x迁移时，您可以继续将内容加密密钥存储在LiveCycleES数据库中，或实施自定义解决方案以将内容加密密钥安全地存储在其他位置。 如果决定将内容加密密钥存储在LiveCycleESLiveCycle®库中，请遵循&#x200B;**ES2**&#x200B;中&#x200B;*保护对数据库*&#x200B;中敏感内容的访问权的建议。

有关使用Flash媒体Rights Management服务器1.x确保与打包内容兼容的更多信息，请参阅[Adobe PrimetimeAPI参考](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)上的Adobe PrimetimeDRM API。
