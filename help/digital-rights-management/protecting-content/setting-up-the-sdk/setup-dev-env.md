---
description: 如果要设置Primetime DRM，请从DVD复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，您还需要向Adobe Systems， Incorporated申请证书。 然后，Adobe会向您颁发多个凭据，用于保护打包内容、许可证以及客户端和服务器之间的通信的完整性。
title: 设置开发环境
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 设置开发环境 {#set-up-your-development-environment}

如果要设置Primetime DRM，请从DVD复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，您还需要向Adobe Systems， Incorporated申请证书。 然后，Adobe会向您颁发多个凭据，用于保护打包内容、许可证以及客户端和服务器之间的通信的完整性。

Adobe在DVD上提供Primetime DRM SDK：

1. 从[！DNL]复制以下文件 [DRM DVD]/SDK/]到开发系统（在Java类路径上）：

   * [!DNL adobe-flashaccess-certs.jar]  — 包括Adobe根证书
   * [!DNL adobe-flashaccess-sdk.jar]  — 包含Primetime DRM核心SDK类
   * [!DNL adobe-flashaccess-sdk-pro.jar]  — 包括Primetime DRM Professional SDK课程，仅需要专业功能

1. 从[！DNL]复制以下文件 [DRM DVD]/SDK/thirdparty]到您的开发系统：

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

1. （可选）为了提高性能，您可以通过从[！DNL]复制相应的平台特定库来启用对加密操作的本机支持 [DRM DVD]/SDK/thirdparty/cryptoj/]到您的开发系统（请记得将位置放置到您的路径上）：

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

     >[!NOTE]
     >
     >这些库的32位和64位版本均可用。 只有在具有64位操作系统并且运行64位版本的Java时，才应使用64位版本。

1. （可选）有关AdobeFlash媒体Rights Management服务器(FMRMS) 1.x兼容性的功能，请复制 `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` 到开发系统：

   仅当您以前部署了FMRMS 1.x并且不想重新打包受FMRMS保护的内容时才部署此项。 在这种情况下，您必须将此支持添加到许可证服务器，以便它能够管理旧内容和客户端。
