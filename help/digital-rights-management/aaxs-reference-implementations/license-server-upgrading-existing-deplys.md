---
seo-title: 升级现有部署
title: 升级现有部署
uuid: 57e62a88-e541-435c-8274-7f1602548601
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 升级现有部署{#upgrading-existing-deployments}

要升级运行3.0 Reference Implementation License Server或Watched Folder Packager的服务器，请将部署在应用程序服务器上的[!DNL .war]文件替换为Adobe访问参考Implementation Server附带的文件。

如果您计划使用引用实施许可证服务器进行域注册，则需要几个新的数据库表。 要重新创建整个引用实现数据库，请运行`CreateSampleDB.sql`。 要保留现有数据库记录并添加新表，请打开`CreateSampleDB.sql`并只运行命令以创建以下表：

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

必须向flashaccess-refimpl.properties添加以下属性才能使用域支持：

* `HandlerConfiguration.DomainCAs.n` 或  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password`或  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

必须向[!DNL flashaccess-refimpl.properties]添加以下属性，以支持对iOS客户端进行远程密钥投放:

* `HandlerConfiguration.KeyServerCertificate` 或  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

