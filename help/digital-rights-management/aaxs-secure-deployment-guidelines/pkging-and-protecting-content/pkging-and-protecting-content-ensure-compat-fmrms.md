---
seo-title: 确保与Flash Media Rights Management Server 1.x的兼容性
title: 确保与Flash Media Rights Management Server 1.x的兼容性
uuid: 0160ca02-ebe6-4090-bf32-1d1a46088844
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 确保与Flash Media Rights Management Server 1.x的兼容性{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x和Adobe Access使用不同的元数据打包内容和请求许可证。 要使用FMRMS版本1.x内容，Adobe Access必须转换元数据。

Adobe Access SDK支持两种转换元数据的选项：

* 脱机（建议）

   在脱机流程中生成Adobe Access元数据，并存储该元数据以在客户端请求时使用。 Adobe建议使用此选项。 如果元数据是脱机生成的，则许可证服务器不需要访问1.x CEK或打包程序凭据。 此外，脱机转换可提供更好的性能，因为许可证服务器不需要实时生成元数据。

* 按需

   在客户端请求Adobe Access元数据时，按需生成该元数据。 当Adobe Access客户端下载版本1.x内容时，它会将DRM元数据（也称为DRM头）发送到Adobe Access SDK。 SDK会将DRM元数据转换为当前格式。 SDK加密内容加密密钥(CEK)并将其嵌入到元数据中，并将内容发送回Adobe Access客户端。 （Adobe Access 1.x元数据不包含CEK。）

   要转换元数据，Adobe Access需要访问Adobe Access 1.x内容加密密钥。 从Flash Media Rights Management Server 1.x迁移时，您可以继续将内容加密密钥存储在LiveCycle ES数据库中，也可以实施自定义解决方案以安全地将内容加密密钥存储在其他位置。 如果选择继续将内容加密密钥存储在LiveCycle ES数据库中，请遵循Reharding and Security for LiveCycle ES中的“保护对数据库中敏感内容的访问”中所述的建议 **。

有关确保与使用Flash Media Rights Management Server 1.x打包的内容兼容的更多信息，请参阅 *Adobe Access API参考*。
