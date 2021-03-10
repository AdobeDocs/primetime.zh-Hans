---
description: 要升级支持版本3.0 Reference Implementation License Server或Watched Folder Packager的服务器，您需要用Adobe Primetime DRM Reference Implementation Server附带的文件替换在应用程序服务器上部署的.war文件。
title: 升级现有部署
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 概述{#upgrade-existing-deployments-overview}

要升级支持版本3.0 Reference Implementation License Server或Watched Folder Packager的服务器，您需要用Adobe Primetime DRM Reference Implementation Server附带的文件替换在应用程序服务器上部署的.war文件。

要使用引用实施许可证服务器进行域注册，需要几个新的数据库表。 您需要重新创建整个引用实现数据库并运行`CreateSampleDB.sql`。

要保留数据库记录并添加新表，请执行以下操作：

1. 打开`CreateSampleDB.sql`并运行创建以下表的命令：

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. 向[!DNL flashaccess-refimpl.properties]添加以下属性以使用域支持：

   * `HandlerConfiguration.DomainCAs.n` 或  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password` 或  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. 将以下属性添加到[!DNL flashaccess-refimpl.properties]以支持向iOS客户端进行远程密钥投放:

   * `HandlerConfiguration.KeyServerCertificate` 或  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`