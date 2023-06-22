---
description: 要设置Adobe®访问™要使用，请从DVD复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，还要向Adobe Systems Incorporated申请证书。 将为您颁发多个凭据，用于保护打包内容、许可证以及客户端和服务器之间的通信的完整性。
title: 设置开发环境
exl-id: 66310fc8-7513-4aab-81d6-1370ce216cbf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 设置SDK {#setting-up-the-sdk}

要设置Adobe®访问™要使用，请从DVD复制文件。 这些文件包括包含代码、证书和第三方类的JAR文件。 此外，还要向Adobe Systems Incorporated申请证书。 将为您颁发多个凭据，用于保护打包内容、许可证以及客户端和服务器之间的通信的完整性。

Adobe访问SDK有两种类型：
* ADOBE ACCESS CORE SDK
* ADOBE ACCESS PROFESSIONAL SDK

下表显示了Adobe访问SDK的基本比较：

| 功能 | ADOBE ACCESS CORE SDK | ADOBE ACCESS PROFESSIONAL SDK |
|---|---|---|
| Flash Access2.0功能 | 可用 | 可用 |
| 密钥轮替 | - | 可用 |
| 域支持 | 可用 | 可用 |
| 增强型许可证链接 | 可用 | 可用 |
| 同步消息 | 可用 | 可用 |
| 许可证预生成 | 可用 | 可用 |
| 嵌入式许可证 | 可用 | 可用 |

## 设置开发环境 {#setting-up-the-development-environment}

从DVD中，复制以下SDK文件，以便在开发环境和Java类路径中使用：

* adobe-flashaccess-certs.jar(包含Adobe根证书)
* adobe-flashaccess-sdk.jar(包含Adobe Access Core SDK类)
* adobe-flashaccess-sdk-pro.jar(包含Adobe Access Professional SDK类，仅专业功能需要这些类)

您还需要以下第三方JAR文件，这些文件也位于SDK的“第三方”文件夹中的DVD上：

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

为了提高性能，您可以选择通过部署位于SDK的“第三方/cryptoj”文件夹中的平台特定库来启用对加密操作的本机支持。 要启用本机支持，请将平台的库（适用于Windows的jsafe.dll或适用于Linux的libjsafe.so）添加到路径中。 提供了这些库的32位和64位版本。 （请注意，只有在具有64位操作系统且运行64位版本的Java时，才应使用64位版本）。

此外，SDK的一个可选部分是adobe-flashaccess-lcrm.jar。 只有与AdobeFlash媒体Rights Management服务器(FMRMS) 1.x兼容性相关的功能才需要此文件。 如果您之前部署了FMRMS 1.x，并且不想重新打包受FMRMS保护的内容，则必须向许可证服务器添加支持，以便它能够处理旧内容和客户端。
