---
description: 您可以在许可证获取期间调用自定义授权逻辑，以确定是否应向请求客户端颁发许可证。
title: 自定义授权扩展
exl-id: dbdda9c6-32bf-4904-981f-0029bf0a82f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# 自定义授权扩展{#custom-authorization-extensions}

您可以在许可证获取期间调用自定义授权逻辑，以确定是否应向请求客户端颁发许可证。

如果您想实施自己的客户授权扩展，则必须首先查看 [!DNL SampleAuthorizer.java] 位于samples目录中的示例代码。 此示例的编译版本位于 [!DNL flashaccess-license-server-ext-sample.jar].

如果您想要构建自己的扩展，则需要实施 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 界面并确保 [!DNL flashaccess-license-server-exts.jar] 和 [!DNL commons-logging.jar] 在生成路径中( [!DNL adobe-flashaccess-sdk.jar] 此外，如果您使用以下对象中的某些字段， `IMessageFacade`)。

如果要部署扩展，需要将jar或类文件复制到 *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

如果要更新jar或类文件，则需要先重新启动服务器，然后才能使用更新的版本。 您还必须将授权程序类名添加到租户配置文件中。
