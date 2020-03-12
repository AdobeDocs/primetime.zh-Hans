---
description: 要升级支持3.0参考实施许可证服务器或监视文件夹打包程序的服务器，您需要将在应用程序服务器上部署的。war文件替换为Adobe Primetime DRM参考实施服务器附带的文件。
seo-description: 要升级支持3.0参考实施许可证服务器或监视文件夹打包程序的服务器，您需要将在应用程序服务器上部署的。war文件替换为Adobe Primetime DRM参考实施服务器附带的文件。
seo-title: 升级现有部署
title: 升级现有部署
uuid: 1a40aae9-f639-41fa-b42d-cf8cdfcde694
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 概述 {#upgrade-existing-deployments-overview}

要升级支持3.0参考实施许可证服务器或监视文件夹打包程序的服务器，您需要将在应用程序服务器上部署的。war文件替换为Adobe Primetime DRM参考实施服务器附带的文件。

要使用参考实施许可证服务器进行域注册，需要几个新的数据库表。 您需要重新创建整个参考实现数据库并运行 `CreateSampleDB.sql`。

要保留数据库记录并添加新表，请执行以下操作：

1. 打开 `CreateSampleDB.sql` 和运行创建以下表的命令：

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. 添加以下属性以 [!DNL flashaccess-refimpl.properties] 使用域支持：

   * `HandlerConfiguration.DomainCAs.n` os `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password` 或 `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. 添加以下属性以 [!DNL flashaccess-refimpl.properties] 支持向iOS客户端远程密钥交付：

   * `HandlerConfiguration.KeyServerCertificate` os `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`