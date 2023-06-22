---
title: 自定义授权扩展
description: 在许可证获取期间可以调用自定义授权逻辑以确定是否应该向请求客户端颁发许可证。
exl-id: bf7870f5-11bf-4392-a422-506b47d684f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 自定义授权扩展 {#custom-authorization-extensions}

在许可证获取期间可以调用自定义授权逻辑以确定是否应该向请求客户端颁发许可证。

要实施您自己的客户授权扩展，请首先查看 [!DNL SampleAuthorizer.java] 位于samples目录中的示例代码（此示例的编译版本位于flashaccess-license-server-ext-sample.jar中）。

要构建您自己的扩展，请实施 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 界面并确保 `flashaccess-license-server-exts.jar` 和 `commons-logging.jar` 在生成路径上 `adobe-flashaccess-sdk.jar` 如果您使用中的某些字段，则必须位于构建路径上 `IMessageFacade`)。 要部署扩展，请将jar或类文件复制到 *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. 如果需要更新jar或类文件，则必须先重新启动服务器，然后才能使用更新的版本。 您还必须将授权程序类名添加到租户配置文件中。
