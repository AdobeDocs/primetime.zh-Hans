---
title: 确保与Flash Media Rights Management Server 1.x的兼容性
description: 确保与Flash Media Rights Management Server 1.x的兼容性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# 确保与Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}的兼容性

Flash Media Rights Management Server 1.x和Adobe Access使用不同的元数据打包内容和请求许可证。 要使Adobe访问使用FMRMS 1.x版内容，必须转换元数据。

Adobe Access SDK支持两种转换元数据的选项：

* 脱机（推荐）

   在脱机流程中生成Adobe访问元数据，并存储该元数据以供客户端请求时使用。 Adobe建议使用此选项。 如果元数据是脱机生成的，则许可证服务器不需要访问1.x CEK或打包程序凭据。 此外，转换脱机优惠的性能更好，因为许可证服务器不需要实时生成元数据。

* 按需

   在客户端请求Adobe访问元数据时，按需生成数据。 当Adobe Access客户端下载版本1.x内容时，它将DRM元数据（也称为DRM头）发送到Adobe Access SDK。 SDK会将DRM元数据转换为当前格式。 SDK加密内容加密密钥(CEK)并将其嵌入到元数据中，并将内容发送回Adobe Access客户端。 (Adobe访问1.x元数据不包含CEK。)

   要转换元数据，Adobe访问需要访问Adobe访问1.x内容加密密钥。 从Flash Media Rights Management Server 1.x迁移时，您可以继续将内容加密密钥存储在LiveCycle ES数据库中，也可以实施自定义解决方案以将内容加密密钥安全地存储到其他位置。 如果选择继续将内容加密密钥存储在LiveCycle ES数据库中，请遵循&#x200B;*针对LiveCycle ES*&#x200B;强化和安全中的“保护对数据库中敏感内容的访问”中概述的建议。

有关确保与使用Flash Media Rights Management Server 1.x打包的内容兼容的详细信息，请参阅&#x200B;*Adobe访问API参考*。
