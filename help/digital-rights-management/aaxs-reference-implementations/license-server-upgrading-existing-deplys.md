---
title: 升级现有部署
description: 升级现有部署
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 升级现有部署 {#upgrading-existing-deployments}

要升级运行3.0版参考实施许可证服务器或Watched文件夹打包程序的服务器，请替换 [!DNL .war] 使用Application Server Access Reference Implementation Server附带的文件在Adobe服务器上部署的文件。

如果打算将域注册与参考实施许可证服务器一起使用，则需要几个新的数据库表。 要重新创建整个参考实施数据库，请运行 `CreateSampleDB.sql`. 要保留现有数据库记录并添加新表，请打开 `CreateSampleDB.sql`并仅运行命令创建以下表：

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
