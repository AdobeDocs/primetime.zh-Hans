---
seo-title: 自定义授权扩展
title: 自定义授权扩展
description: 在获取许可证期间可以调用自定义授权逻辑来决定是否应向请求客户端发放许可证。
seo-description: 在获取许可证期间可以调用自定义授权逻辑来决定是否应向请求客户端发放许可证。
uuid: fb40db6f-30aa-46e3-9eeb-faff3cfedab1
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0

---


# 自定义授权扩展 {#custom-authorization-extensions}

在获取许可证期间可以调用自定义授权逻辑来决定是否应向请求客户端发放许可证。

要实现您自己的客户授权扩展，请首先查看位于示例目录中的示例代码（此示例的编译版本位于flashaccess-license-server-ext-sample.jar中）。 [!DNL SampleAuthorizer.java]

要构建您自己的扩展，请实 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 施界面并确保在构建路径上 `flashaccess-license-server-exts.jar` ，并且在构建路径上也必须 `commons-logging.jar` 位于构建路径上（如果您在中使用了某些字段） `adobe-flashaccess-sdk.jar``IMessageFacade`。 要部署扩展，请将您的jar或类文件复制到 *LicenseServer.ConfigRoot*`/flashaccessserver/libs`。 如果需要更新jar或类文件，则必须在使用更新版本之前重新启动服务器。 您还必须将授权者类名称添加到租户配置文件。
