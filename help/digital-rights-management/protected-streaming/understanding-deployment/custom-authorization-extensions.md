---
description: 您可以在获取许可证期间调用自定义授权逻辑，以决定是否应将许可证颁发给请求客户端。
title: 自定义授权扩展
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# 自定义授权扩展{#custom-authorization-extensions}

您可以在获取许可证期间调用自定义授权逻辑，以决定是否应将许可证颁发给请求客户端。

如果要实施您自己的客户授权扩展，必须首先查看位于samples目录中的[!DNL SampleAuthorizer.java]示例代码。 此示例的编译版本位于[!DNL flashaccess-license-server-ext-sample.jar]中。

如果要构建自己的扩展，您需要实现`com.adobe.flashaccess.server.license.extension.auth.IAuthorizer`接口，并确保[!DNL flashaccess-license-server-exts.jar]和[!DNL commons-logging.jar]位于构建路径中（如果使用`IMessageFacade`中的某些字段，[!DNL adobe-flashaccess-sdk.jar]也必须位于构建路径中）。

如果要部署扩展，您需要将jar或类文件复制到&#x200B;*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs]。

如果要更新jar或类文件，则需要在使用更新后的版本之前重新启动服务器。 您还必须将授权程序类名称添加到租户配置文件。
