---
description: 要设置Adobe® Access™以供使用，请从DVD中复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，请求Adobe Systems Incorporated的证书。 您将获得多个凭据，用于保护打包内容、许可证的完整性以及客户端与服务器之间的通信。
seo-description: 要设置Adobe® Access™以供使用，请从DVD中复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，请求Adobe Systems Incorporated的证书。 您将获得多个凭据，用于保护打包内容、许可证的完整性以及客户端与服务器之间的通信。
seo-title: 设置开发环境
title: 设置开发环境
uuid: 1f192783-9c9a-4342-909a-4881248a85ad
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# 设置SDK {#setting-up-the-sdk}

要设置Adobe® Access™以供使用，请从DVD中复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，请求Adobe Systems Incorporated的证书。 您将获得多个凭据，用于保护打包内容、许可证的完整性以及客户端与服务器之间的通信。

Adobe访问SDK有两种类型：
* Adobe Access CoreSDK
* Adobe Access ProfessionalSDK

下表显示了Adobe访问SDK的基本比较：

| 功能 | Adobe Access CoreSDK | Adobe Access ProfessionalSDK |
|---|---|---|
| Flash Access2.0功能 | 可用 | 可用 |
| 键旋转 | - | 可用 |
| 域支持 | 可用 | 可用 |
| 增强的许可证链接 | 可用 | 可用 |
| 同步消息 | 可用 | 可用 |
| 许可预生成 | 可用 | 可用 |
| 嵌入式许可 | 可用 | 可用 |

## 设置开发环境{#setting-up-the-development-environment}

从DVD中复制以下SDK文件，以便在开发环境和Java类路径中使用：

* adobe-flashaccess-certs.jar(包含Adobe根证书)
* adobe-flashaccess-sdk.jar(包含Adobe Access CoreSDK类)
* adobe-flashaccess-sdk-pro.jar(包含Adobe Access ProfessionalSDK类，仅专业版功能需要)

您还需要SDK的“第三方”文件夹中DVD上的以下第三方JAR文件：

* bcmail-jdk15-141.jar
* bcprov-jdk15-141.jar
* commons-discovery-0.4.jar
* commons-logging-1.1.1.jar
* cryptoj.jar
* jaxb-api.jar
* jaxb-impl.jar
* jaxb-libs.jar
* relaxngDatatype.jar
* rm-pdrl.jar
* xsdlib.jar

为了提高性能，您可以选择通过部署位于SDK的“thirdparty/cryptoj”文件夹中的平台特定库来启用对加密操作的本机支持。 要启用本机支持，请将平台的库（适用于Windows的jsafe.dll或适用于Linux的libjsafe.so）添加到路径中。 提供这些库的32位和64位版本。 （请注意，仅当您有64位操作系统并且运行64位版本的Java时，才应使用64位版本。）

此外，SDK的可选部分是adobe-flashaccess-lcrm.jar。 只有与AdobeFlash媒体Rights Management服务器(FMRMS)1.x兼容性相关的功能才需要此文件。 如果您以前部署了FMRMS 1.x，但不想重新打包受FMRMS保护的内容，则必须向许可证服务器添加支持，这样它才能处理旧内容和客户端。
