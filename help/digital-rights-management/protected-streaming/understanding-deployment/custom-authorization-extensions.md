---
description: 您可以在许可证获取期间调用自定义授权逻辑，以确定是否应将许可证颁发给请求客户端。
title: 自定义授权扩展
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# 自定义授权扩展{#custom-authorization-extensions}

您可以在许可证获取期间调用自定义授权逻辑，以确定是否应将许可证颁发给请求客户端。

如果您想要实施自己的客户授权扩展，则必须首先查看 [!DNL SampleAuthorizer.java] 位于samples目录中的示例代码。 此示例的编译版本位于 [!DNL flashaccess-license-server-ext-sample.jar].

如果您想要构建自己的扩展，则需要实施 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 界面并确保 [!DNL flashaccess-license-server-exts.jar] 和 [!DNL commons-logging.jar] 在生成路径中( [!DNL adobe-flashaccess-sdk.jar] 如果您在中使用某些字段，则还必须位于生成路径中 `IMessageFacade`)。

如果要部署扩展，则需要将jar或类文件复制到 *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

如果要更新jar或类文件，则需要先重新启动服务器，然后才能使用更新的版本。 您还必须将授权程序类名添加到租户配置文件中。
