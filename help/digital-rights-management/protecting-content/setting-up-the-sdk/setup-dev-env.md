---
description: 如果要设置Primetime DRM，请从DVD中复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，您还需要从Adobe Systems, Incorporated请求证书。 然后，Adobe会向您发布多个凭据，用于保护打包内容、许可证的完整性以及客户端与服务器之间的通信。
seo-description: 如果要设置Primetime DRM，请从DVD中复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，您还需要从Adobe Systems, Incorporated请求证书。 然后，Adobe会向您发布多个凭据，用于保护打包内容、许可证的完整性以及客户端与服务器之间的通信。
seo-title: 设置开发环境
title: 设置开发环境
uuid: 68afefe8-7ec6-466e-89a8-bc0da8afb4c8
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 设置开发环境 {#set-up-your-development-environment}

如果要设置Primetime DRM，请从DVD中复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，您还需要从Adobe Systems, Incorporated请求证书。 然后，Adobe会向您发布多个凭据，用于保护打包内容、许可证的完整性以及客户端与服务器之间的通信。

Adobe提供Primetime DRM SDK on DVD:

1. 将以下文件从[!DNL [DRM DVD]/SDK/]复制到开发系统（在Java类路径上）:

   * [!DNL adobe-flashaccess-certs.jar] -包括Adobe根证书
   * [!DNL adobe-flashaccess-sdk.jar] -包括Primetime DRM核心SDK类
   * [!DNL adobe-flashaccess-sdk-pro.jar] -包括Primetime DRM Professional SDK类，仅专业功能需要

1. 将以下文件从[!DNL [DRM DVD]/SDK/thirdparty]复制到开发系统：

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

1. （可选）为了提高性能，您可以通过将相应的平台特定库从[!DNL [DRM DVD]/SDK/thirdparty/cryptoj/]复制到开发系统中来启用对加密操作的本机支持（请记住将位置放在您的路径上）:

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >提供这些库的32位和64位版本。 仅当您有64位操作系统并且运行64位版本的Java时，才应使用64位版本。

1. （可选）要获得与Adobe Flash Media Rights Management Server(FMRMS)1.x兼容性相关的功能，请复制到您 `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` 的开发系统：

   仅当您之前部署了FMRMS 1.x并且不想重新打包受FMRMS保护的内容时，才部署此组件。 在这种情况下，您必须向许可证服务器添加此支持，以便它能够管理旧内容和客户端。
