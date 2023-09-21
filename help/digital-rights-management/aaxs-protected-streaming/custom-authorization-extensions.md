---
title: 自定义授权扩展
description: 在许可证获取期间可以调用自定义授权逻辑以确定是否应该向请求客户端颁发许可证。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 自定义授权扩展 {#custom-authorization-extensions}

在许可证获取期间可以调用自定义授权逻辑以确定是否应该向请求客户端颁发许可证。

要实施您自己的客户授权扩展，请首先查看 [!DNL SampleAuthorizer.java] 示例代码位于samples目录中（此示例的编译版本位于flashaccess-license-server-ext-sample.jar）。

要构建您自己的扩展，请实施 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 界面并确保 `flashaccess-license-server-exts.jar` 和 `commons-logging.jar` 在生成路径上 `adobe-flashaccess-sdk.jar` 如果您利用中的某些字段，则必须位于生成路径上 `IMessageFacade`)。 要部署扩展，请将jar或类文件复制到 *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. 如果需要更新jar或类文件，则必须先重新启动服务器，然后才能使用更新的版本。 您还必须将授权程序类名添加到租户配置文件中。
