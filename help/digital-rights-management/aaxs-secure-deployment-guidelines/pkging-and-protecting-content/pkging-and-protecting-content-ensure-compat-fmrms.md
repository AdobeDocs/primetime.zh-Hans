---
title: 确保与Flash MediaRights Management服务器1.x兼容
description: 确保与Flash MediaRights Management服务器1.x兼容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 确保与Flash MediaRights Management服务器1.x兼容{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash媒体Rights Management服务器1.x和Adobe访问使用不同的元数据来打包内容和请求许可证。 要使Adobe访问使用FMRMS版本1.x的内容，必须转换元数据。

Adobe访问SDK支持两种转换元数据的选项：

* 离线（推荐）

  在脱机进程中生成Adobe访问元数据，并将其存储以供客户端请求时使用。 Adobe建议使用此选项。 如果元数据是离线生成的，则许可证服务器不需要访问1.x CEK或打包程序凭据。 此外，离线转换可提供更好的性能，因为许可证服务器不需要实时生成元数据。

* On-demand

  在客户端请求Adobe访问元数据时按需生成该元数据。 当Adobe访问客户端下载版本1.x内容时，它会将DRM元数据（也称为DRM标头）发送到Adobe访问SDK。 SDK会将DRM元数据转换为当前格式。 SDK对内容加密并将内容加密密钥(CEK)嵌入到元数据中，并将内容发送回Adobe访问客户端。 (Adobe访问1.x元数据不包含CEK。)

  要转换元数据，Adobe访问需要访问Adobe访问1.x内容加密密钥。 从Flash媒体Rights Management服务器1.x迁移时，您可以继续将内容加密密钥存储在LiveCycleES数据库中，也可以实施自定义解决方案以将内容加密密钥安全地存储在其他位置。 如果选择继续将内容加密密钥存储在LiveCycleES数据库中，请遵循以下部分中列出的建议：保护对数据库中敏感内容的访问 *LiveCycleES的强化和安全性*.

有关确保与使用Flash MediaRights Management服务器1.x打包的内容兼容的更多信息，请参阅 *Adobe访问API参考*.
