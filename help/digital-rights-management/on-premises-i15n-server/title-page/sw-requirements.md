---
title: 软件要求
description: 软件要求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 软件要求 {#software-requirements}

* Tomcat 6
* JDK 1.8

## 代码交付/包内容{#code-delivery-package-contents}

Adobe Primetime DRM On Premises Individualization Server包包含以下内容：

* [!DNL flashaccess.war]  — 个性化服务器
* [!DNL flashaccess-kgs.war]  — 可选的密钥生成服务器
* [!DNL /shared]  — 包含：

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties]  — 示例属性文件

* [!DNL thirdparty/]  — 包括将Crypto-J支持作为本机库：

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar]  — 用于加密服务器凭据密码的实用程序
* [!DNL ROOT]  — 包含 [!DNL crossdomain.xml] 文件

* ECI缓存文件 — 已预下载
* [!DNL addIndivCert.py]  — 用于更新许可证服务器的信任根以支持本地个性化的脚本
* [!DNL CreateMetadata.jar]  — 用于创建本地DRM元数据的实用程序
* [!DNL client_sample/]  — 包含客户端代码片段的文件夹
* 发行说明 — 在最后一分钟对文档的任何补充

## 获取个性化服务器证书{#obtain-individualization-server-certificates}

要使用On Premises Individualization Server，您必须首先获取两个数字凭据（证书）：

* *个性化传输凭据*  — 由Adobe颁发
* *个性化CA凭据*  — 由Symantec (VeriSign)颁发

要获取这些证书，请通过Zendesk票证将请求提交到： [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

请注意，这些凭据是运行Primetime DRM许可证服务器所需的凭据之外的凭据。
