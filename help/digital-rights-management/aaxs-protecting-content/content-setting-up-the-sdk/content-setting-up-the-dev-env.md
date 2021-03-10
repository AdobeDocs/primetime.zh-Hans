---
description: 要设置Adobe® Access™以供使用，请从DVD中复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，请求Adobe Systems Incorporated的证书。 您将获得多个凭据，用于保护打包内容、许可证的完整性以及客户端与服务器之间的通信。
title: 设置开发环境
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# 设置SDK {#setting-up-the-sdk}

要设置Adobe® Access™以供使用，请从DVD中复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，请求Adobe Systems Incorporated的证书。 您将获得多个凭据，用于保护打包内容、许可证的完整性以及客户端与服务器之间的通信。

Adobe访问SDK有两种类型：
* Adobe Access Core SDK
* Adobe Access Professional SDK

下表显示了Adobe Access SDK的基本比较：

| 功能 | Adobe Access Core SDK | Adobe Access Professional SDK |
|---|---|---|
| Flash Access 2.0功能 | 可用 | 可用 |
| 键旋转 | - | 可用 |
| 域支持 | 可用 | 可用 |
| 增强的许可证链接 | 可用 | 可用 |
| 同步消息 | 可用 | 可用 |
| 许可预生成 | 可用 | 可用 |
| 嵌入式许可 | 可用 | 可用 |

## 设置开发环境{#setting-up-the-development-environment}

从DVD中，复制以下SDK文件以用于开发环境和Java类路径：

* adobe-flashaccess-certs.jar(包含Adobe根证书)
* adobe-flashaccess-sdk.jar(包含Adobe Access Core SDK类)
* adobe-flashaccess-sdk-pro.jar(包含Adobe Access Professional SDK类，仅专业版功能需要)

您需要以下第三方JAR文件（也位于SDK的“第三方”文件夹的DVD中）：

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

为了提高性能，您可以通过部署位于SDK的“thirdparty/cryptoj”文件夹中的特定平台库，选择启用对加密操作的本机支持。 要启用本机支持，请将平台的库（适用于Windows的jsafe.dll或适用于Linux的libjsafe.so）添加到路径中。 提供了这些库的32位和64位版本。 （请注意，仅当您有64位操作系统并且运行64位版本的Java时，才应使用64位版本）。

此外，SDK的一个可选部分是adobe-flashaccess-lcrm.jar。 只有与Adobe Flash Media Dibation Server(FMRMS)1.x兼容性相关的功能才需要此文件。 如果您之前部署了FMRMS 1.x，但不想重新打包受FMRMS保护的内容，则必须向许可证服务器添加支持，以便它能够处理旧内容和客户端。
