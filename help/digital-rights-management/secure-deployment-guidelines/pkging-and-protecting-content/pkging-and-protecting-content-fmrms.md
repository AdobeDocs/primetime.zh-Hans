---
description: Flash Media Rights Management Server 1.x和Adobe Primetime DRM使用不同的元数据打包内容和请求许可证。 要使Primetime DRM使用FMRMS版本1.x内容，必须转换元数据。
seo-description: Flash Media Rights Management Server 1.x和Adobe Primetime DRM使用不同的元数据打包内容和请求许可证。 要使Primetime DRM使用FMRMS版本1.x内容，必须转换元数据。
seo-title: 确保与Flash Media Rights Management Server 1.x的兼容性
title: 确保与Flash Media Rights Management Server 1.x的兼容性
uuid: dd70941e-9015-4fb0-b265-557b6252e051
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 确保与Flash Media Rights Management Server 1.x的兼容性 {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x和Adobe Primetime DRM使用不同的元数据打包内容和请求许可证。 要使Primetime DRM使用FMRMS版本1.x内容，必须转换元数据。

Primetime DRM SDK支持以下元数据转换选项：

* 脱机（建议）

   在脱机流程中生成Primetime DRM元数据，并存储元数据，直到客户端请求它。 如果元数据是脱机生成的，则许可证服务器不需要访问1.x CEK或打包程序凭据。 脱机转换可提供更好的性能，因为许可证服务器无需实时生成元数据。
* 按需

   Primetime DRM元数据是在客户端请求元数据时生成的。 当Primetime DRM客户端下载版本1.x内容时，客户端将DRM元数据发送到Primetime DRM SDK。 SDK将DRM元数据转换为当前格式，加密内容加密密钥(CEK)并将其嵌入到元数据中，并将内容发送回Primetime DRM客户端。

   >[!NOTE]
   >
   >Primetime DRM 1.x元数据不包括CEK。

   要转换元数据，Primetime DRM需要访问Primetime DRM 1.x内容加密密钥。 从Flash Media Rights Management Server 1.x迁移时，您可以继续将内容加密密钥存储在LiveCycle ES数据库中，或实施自定义解决方案以将内容加密密钥安全地存储在其他位置。 如果决定将内容加密密钥存储在LiveCycle ES数据库中，请遵循 *Hardening and Security for LiveCycle® ES2中保护对数据库中敏感内容的访问中所述的建议*****。

有关确保与使用Flash Media Rights Management Server 1.x打包的内容兼容的更多信息，请参阅 [Adobe Primetime API参考的Adobe Primetime DRM API](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)。
