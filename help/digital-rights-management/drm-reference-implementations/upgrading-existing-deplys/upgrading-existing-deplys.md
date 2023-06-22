---
description: 要升级支持3.0版Reference Implementation License Server或Watched Folder Packager的服务器，您需要将已部署在应用程序服务器上的.war文件替换为Adobe Primetime DRM Reference Implementation Server附带的文件。
title: 升级现有部署
exl-id: 83edaf0a-e527-470d-8b8d-23e5ba86b039
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 概述 {#upgrade-existing-deployments-overview}

要升级支持3.0版Reference Implementation License Server或Watched Folder Packager的服务器，您需要将已部署在应用程序服务器上的.war文件替换为Adobe Primetime DRM Reference Implementation Server附带的文件。

要将域注册用于参考实施许可证服务器，需要几个新的数据库表。 您需要重新创建整个参考实施数据库并运行 `CreateSampleDB.sql`.

要保留数据库记录并添加新表，请执行以下操作：

1. 打开 `CreateSampleDB.sql` 和运行创建以下表的命令：

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. 将以下属性添加到 [!DNL flashaccess-refimpl.properties] 要使用域支持，请执行以下操作：

   * `HandlerConfiguration.DomainCAs.n` 或 `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password` 或 `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. 将以下属性添加到 [!DNL flashaccess-refimpl.properties] 要支持将远程密钥交付到iOS客户端，请执行以下操作：

   * `HandlerConfiguration.KeyServerCertificate` 或 `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
