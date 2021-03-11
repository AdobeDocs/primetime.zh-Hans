---
title: 升级现有部署
description: 升级现有部署
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 升级现有部署{#upgrading-existing-deployments}

要升级运行3.0 Reference Implementation License Server或Watched Folder Packager的服务器，请将部署在Application Server上的[!DNL .war]文件替换为Adobe Access Reference Implementation Server附带的文件。

如果您计划使用引用实施许可证服务器进行域注册，则需要多个新的数据库表。 要重新创建整个参考实现数据库，请运行`CreateSampleDB.sql`。 要保留现有数据库记录并添加新表，请打开`CreateSampleDB.sql`并仅运行命令以创建以下表：

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

必须向flashaccess-refimpl.properties添加以下属性才能使用域支持：

* `HandlerConfiguration.DomainCAs.n` 或  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password`，或  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

必须向[!DNL flashaccess-refimpl.properties]添加以下属性，以支持向iOS客户端进行远程密钥投放:

* `HandlerConfiguration.KeyServerCertificate` 或  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

