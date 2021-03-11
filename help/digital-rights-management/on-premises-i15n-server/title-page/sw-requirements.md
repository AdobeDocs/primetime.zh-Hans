---
title: 软件要求
description: 软件要求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 软件要求{#software-requirements}

* Tomcat 6
* JDK 1.8

## 代码投放/包内容{#code-delivery-package-contents}

Adobe Primetime DRM On Premiess Indelication Server包包含以下内容：

* [!DNL flashaccess.war]  — 个性化服务器
* [!DNL flashaccess-kgs.war]  — 可选的密钥生成服务器
* [!DNL /shared]  — 包含：

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties]  — 示例属性文件

* [!DNL thirdparty/]  — 将Crypto-J支持作为本机库包括：

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar]  — 用于加密服务器凭据密码的实用程序
* [!DNL ROOT]  — 包含文 [!DNL crossdomain.xml] 件

* ECI缓存文件 — 预下载
* [!DNL addIndivCert.py]  — 用于更新许可证服务器的信任根以支持本地个性化的脚本
* [!DNL CreateMetadata.jar]  — 用于创建本地DRM元数据的实用程序
* [!DNL client_sample/]  — 包含客户端代码片段的文件夹
* 发行说明 — 对于文档的任何最后添加内容

## 获取个性化服务器证书{#obtain-individualization-server-certificates}

要使用内部部署个性化服务器，您必须首先获得两个数字凭据（证书）：

* *个人化运输凭证*  — 由Adobe颁发
* *个性化CA凭据*  — 由Symantec(VeriSign)颁发

要获取这些证书，请通过Zendesk票证向以下用户提交请求：[https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

请注意，这些凭据是运行Primetime DRM许可证服务器所需的凭据之外的凭据。