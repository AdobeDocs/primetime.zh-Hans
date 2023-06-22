---
description: 如果要设置Primetime DRM，请从DVD复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，您还需要从Adobe Systems， Incorporated申请证书。 然后，Adobe会向您颁发多个凭据，用于保护已打包内容的完整性、许可证以及客户端和服务器之间的通信。
title: 设置开发环境
exl-id: c10f85b6-84bc-444f-9001-f49dc88cf99c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 设置开发环境 {#set-up-your-development-environment}

如果要设置Primetime DRM，请从DVD复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，您还需要从Adobe Systems， Incorporated申请证书。 然后，Adobe会向您颁发多个凭据，用于保护已打包内容的完整性、许可证以及客户端和服务器之间的通信。

Adobe在DVD上提供Primetime DRM SDK：

1. 从[！DNL]复制以下文件 [DRM DVD]/SDK/]到开发系统（在Java类路径上）：

   * [!DNL adobe-flashaccess-certs.jar]  — 包含Adobe根证书
   * [!DNL adobe-flashaccess-sdk.jar]  — 包含Primetime DRM核心SDK类
   * [!DNL adobe-flashaccess-sdk-pro.jar]  — 包括Primetime DRM Professional SDK课程，只有专业功能才需要

1. 从[！DNL]复制以下文件 [DRM DVD]/SDK/thirdparty]到开发系统：

   * [!DNL bcmail-jdk15-141.jar]
   * [!DNL bcprov-jdk15-141.jar]
   * [!DNL commons-discovery-0.4.jar]
   * [!DNL commons-logging-1.1.1.jar]
   * [!DNL cryptoj.jar]
   * [!DNL jaxb-api.jar]
   * [!DNL jaxb-impl.jar]
   * [!DNL jaxb-libs.jar]
   * [!DNL relaxngDatatype.jar]
   * [!DNL rm-pdrl.jar]
   * [!DNL xsdlib.jar]
   * [!DNL jackson-annotations-2.4.0-rc4-20140522.175222-3.jar]
   * [!DNL jackson-core--2.4.0-rc4-20140529.184520-13.jar]
   * [!DNL jackson-databind-2.4.0-rc4-20140603.005043-38.jar]

1. （可选）为了提高性能，您可以通过从[！DNL]复制相应的平台特定库来启用对加密操作的本机支持 [DRM DVD]/SDK/thirdparty/cryptoj/]到您的开发系统（请记住将该位置放置在您的路径上）：

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >这些库的32位和64位版本可用。 只有当您具有64位操作系统并运行64位版本的Java时，才应使用64位版本。

1. （可选）有关AdobeFlash媒体Rights Management服务器(FMRMS) 1.x兼容性的功能，请复制 `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` 到开发系统：

   仅当您之前部署了FMRMS 1.x并且不想重新打包受FMRMS保护的内容时才部署此项。 在这种情况下，您必须将此支持添加到许可证服务器，以便它可以管理旧内容和客户端。
