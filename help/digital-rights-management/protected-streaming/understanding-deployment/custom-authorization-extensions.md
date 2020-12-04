---
description: 您可以在获取许可证期间调用自定义授权逻辑，以决定是否应向请求的客户端颁发许可证。
seo-description: 您可以在获取许可证期间调用自定义授权逻辑，以决定是否应向请求的客户端颁发许可证。
seo-title: 自定义授权扩展
title: 自定义授权扩展
uuid: 588b05e5-3402-4586-bbd4-58b7e9a58ee4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# 自定义授权扩展{#custom-authorization-extensions}

您可以在获取许可证期间调用自定义授权逻辑，以决定是否应向请求的客户端颁发许可证。

如果要实施您自己的客户授权扩展，必须首先查看位于示例目录中的[!DNL SampleAuthorizer.java]示例代码。 此示例的编译版本位于[!DNL flashaccess-license-server-ext-sample.jar]中。

如果要构建自己的扩展，您需要实现`com.adobe.flashaccess.server.license.extension.auth.IAuthorizer`接口，并确保[!DNL flashaccess-license-server-exts.jar]和[!DNL commons-logging.jar]位于构建路径中（如果使用`IMessageFacade`中的某些字段，[!DNL adobe-flashaccess-sdk.jar]还必须位于构建路径中）。

如果要部署扩展，您需要将jar或类文件复制到&#x200B;*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs]。

如果要更新jar或类文件，您需要重新启动服务器，然后才能使用更新的版本。 您还必须将授权者类名称添加到租户配置文件。
