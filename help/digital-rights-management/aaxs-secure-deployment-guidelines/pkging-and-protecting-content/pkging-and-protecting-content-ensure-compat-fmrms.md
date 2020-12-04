---
seo-title: 确保与Flash媒体Rights Management服务器1.x的兼容性
title: 确保与Flash媒体Rights Management服务器1.x的兼容性
uuid: 0160ca02-ebe6-4090-bf32-1d1a46088844
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# 确保与Flash媒体Rights Management服务器1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}的兼容性

Flash媒体Rights Management服务器1.x和Adobe访问使用不同的元数据来打包内容和请求许可证。 要使Adobe访问能够使用FMRMS版本1.x内容，必须转换元数据。

Adobe访问SDK支持两种转换元数据的选项：

* 脱机（推荐）

   在脱机流程中生成Adobe访问元数据，并存储该元数据以在客户端请求时使用。 Adobe建议使用此选项。 如果元数据是脱机生成的，则许可证服务器无需访问1.x CEK或打包程序凭据。 此外，转换脱机优惠的性能也更好，因为许可证服务器不需要实时生成元数据。

* 按需

   在客户端请求Adobe访问元数据时，按需生成该元数据。 当Adobe访问客户端下载版本1.x内容时，它会将DRM元数据（也称为DRM头）发送到Adobe访问SDK。 SDK会将DRM元数据转换为当前格式。 SDK加密内容加密密钥(CEK)并将其嵌入到元数据中，并将内容发送回Adobe访问客户端。 (Adobe访问1.x元数据不包含CEK。)

   要转换元数据，Adobe访问需要访问Adobe访问1.x内容加密密钥。 从Flash媒体Rights Management服务器1.x迁移时，您可以继续将内容加密密钥存储在LiveCycleES数据库中，也可以实施自定义解决方案以将内容加密密钥安全地存储在其他位置。 如果选择继续将内容加密密钥存储在LiveCycleESLiveCycle库中，请遵循&#x200B;*ES*&#x200B;强化和安全中的“保护对数据库中敏感内容的访问”中所述的建议。

有关确保与使用Flash媒体Rights Management服务器1.x打包的内容兼容的详细信息，请参阅&#x200B;*Adobe访问API参考*。
