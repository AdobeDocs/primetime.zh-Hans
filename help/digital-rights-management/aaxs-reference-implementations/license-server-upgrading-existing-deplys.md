---
title: 升级现有部署
description: 升级现有部署
copied-description: true
exl-id: e07b883f-d5f7-40d3-9221-a0dc2d859a5a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 升级现有部署 {#upgrading-existing-deployments}

要升级运行3.0版参考实施许可证服务器或Watched Folder Packager的服务器，请更换 [!DNL .war] 使用Adobe访问引用实现服务器随附的文件部署在应用程序服务器上的文件。

如果计划将域注册与参考实施许可证服务器一起使用，则需要几个新的数据库表。 要重新创建整个参考实施数据库，请运行 `CreateSampleDB.sql`. 要保留现有数据库记录并添加新表，请打开 `CreateSampleDB.sql`并只运行命令以创建以下表：

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

必须将以下属性添加到flashaccess-refimpl.properties才能使用域支持：

* `HandlerConfiguration.DomainCAs.n` 或 `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` 和 `DomainRegistrationHandler.ServerCredential.password`，或 `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

必须将以下属性添加到 [!DNL flashaccess-refimpl.properties] 要支持将远程密钥交付到iOS客户端，请执行以下操作：

* `HandlerConfiguration.KeyServerCertificate` 或 `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
