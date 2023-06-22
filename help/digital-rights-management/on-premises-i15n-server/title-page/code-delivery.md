---
title: 代码交付/包内容
description: 代码交付/包内容
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 代码交付/包内容{#code-delivery-package-contents}

Adobe Primetime DRM On Premises Individualization Server包包含以下内容：

* [!DNL flashaccess.war]  — 个性化服务器
* [!DNL flashaccess-kgs.war]  — 可选的密钥生成服务器
* [!DNL /shared]  — 包含：

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties]  — 示例属性文件

* [!DNL thirdparty/]  — 包括作为本机库的Crypto-J支持：

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar]  — 用于加密服务器凭据密码的实用程序
* [!DNL ROOT]  — 包含 [!DNL crossdomain.xml] 文件

* ECI缓存文件 — 预下载
* [!DNL addIndivCert.py]  — 用于更新许可证服务器的信任根以支持内部部署个性化的脚本
* [!DNL CreateMetadata.jar]  — 用于创建本地DRM元数据的实用程序
* [!DNL client_sample/]  — 包含客户端代码片段的文件夹
* 发行说明 — 在最后一刻对文档的任何补充

