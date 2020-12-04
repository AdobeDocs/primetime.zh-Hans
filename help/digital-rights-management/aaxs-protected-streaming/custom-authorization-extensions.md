---
seo-title: 自定义授权扩展
title: 自定义授权扩展
description: 在获取许可证期间可以调用自定义授权逻辑，以决定是否应将许可证颁发给请求客户端。
seo-description: 在获取许可证期间可以调用自定义授权逻辑，以决定是否应将许可证颁发给请求客户端。
uuid: fb40db6f-30aa-46e3-9eeb-faff3cfedab1
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# 自定义授权扩展{#custom-authorization-extensions}

在获取许可证期间可以调用自定义授权逻辑，以决定是否应将许可证颁发给请求客户端。

要实现您自己的客户授权扩展，请首先查看示例目录中的[!DNL SampleAuthorizer.java]示例代码（此示例的编译版本位于flashaccess-license-server-ext-sample.jar中）。

要构建您自己的扩展，请实施`com.adobe.flashaccess.server.license.extension.auth.IAuthorizer`接口，并确保`flashaccess-license-server-exts.jar`和`commons-logging.jar`位于构建路径`adobe-flashaccess-sdk.jar`上，并且如果使用`IMessageFacade`中的某些字段，则还必须位于构建路径上。 要部署扩展，请将jar或类文件复制到&#x200B;*LicenseServer.ConfigRoot* `/flashaccessserver/libs`。 如果需要更新jar或类文件，则必须在使用更新版本之前重新启动服务器。 您还必须将授权者类名称添加到租户配置文件。
