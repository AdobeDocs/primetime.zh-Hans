---
title: 自定义授权扩展
description: 在获取许可证期间可以调用自定义授权逻辑来决定是否应向请求客户端颁发许可证。
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 自定义授权扩展{#custom-authorization-extensions}

在获取许可证期间可以调用自定义授权逻辑来决定是否应向请求客户端颁发许可证。

要实现您自己的客户授权扩展，请首先查看位于samples目录中的[!DNL SampleAuthorizer.java]示例代码（此示例的编译版本位于flashaccess-license-server-ext-sample.jar中）。

要构建您自己的扩展，请实现`com.adobe.flashaccess.server.license.extension.auth.IAuthorizer`接口，并确保`flashaccess-license-server-exts.jar`和`commons-logging.jar`位于构建路径`adobe-flashaccess-sdk.jar`上，如果使用`IMessageFacade`中的某些字段，则还必须位于构建路径上。 要部署扩展，请将您的jar或类文件复制到&#x200B;*LicenseServer.ConfigRoot* `/flashaccessserver/libs`。 如果需要更新jar或类文件，则必须在使用更新版本之前重新启动服务器。 您还必须将授权程序类名称添加到租户配置文件。
