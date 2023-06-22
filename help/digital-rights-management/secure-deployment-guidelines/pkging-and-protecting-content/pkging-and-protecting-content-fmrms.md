---
description: Flash媒体Rights Management服务器1.x和Adobe Primetime DRM使用不同的元数据来打包内容和请求许可证。 要使Primetime DRM使用FMRMS版本1.x内容，必须转换元数据。
title: 确保与Flash MediaRights Management服务器1.x兼容
exl-id: 737c853f-4e27-47e6-9248-857c7800795a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 确保与Flash MediaRights Management服务器1.x兼容 {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash媒体Rights Management服务器1.x和Adobe Primetime DRM使用不同的元数据来打包内容和请求许可证。 要使Primetime DRM使用FMRMS版本1.x内容，必须转换元数据。

Primetime DRM SDK支持以下元数据转换选项：

* 离线（推荐）

   在脱机进程中生成Primetime DRM元数据并存储该元数据，直到客户端请求该元数据为止。 如果元数据是离线生成的，则许可证服务器不需要访问1.x CEK或打包程序凭据。 脱机转换可提供更好的性能，因为许可证服务器不需要实时生成元数据。
* On-demand

   Primetime DRM元数据是在客户端请求元数据时生成的。 当Primetime DRM客户端下载版本1.x内容时，该客户端将DRM元数据发送到Primetime DRM SDK。 SDK将DRM元数据转换为当前格式，加密内容加密密钥(CEK)并将其嵌入元数据中，然后将内容发送回Primetime DRM客户端。

   >[!NOTE]
   >
   >Primetime DRM 1.x元数据不包含CEK。

   要转换元数据，Primetime DRM需要访问Primetime DRM 1.x内容加密密钥。 从Flash媒体Rights Management服务器1.x迁移时，您可以继续将内容加密密钥存储在LiveCycleES数据库中，或实施自定义解决方案以将内容加密密钥安全地存储在其他位置。 如果决定将内容加密密钥存储在LiveCycleES数据库中，请遵循中列出的建议 *保护对数据库中敏感内容的访问* 在 **LiveCycle®ES2的强化和安全性**.

有关确保与使用Flash MediaRights Management服务器1.x打包的内容兼容的更多信息，请参阅上的Adobe Primetime DRM API [Adobe Primetime API参考](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
