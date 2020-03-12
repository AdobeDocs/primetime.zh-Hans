---
description: 您可以在获取许可证期间调用自定义授权逻辑，以决定是否应将许可证颁发给请求客户端。
seo-description: 您可以在获取许可证期间调用自定义授权逻辑，以决定是否应将许可证颁发给请求客户端。
seo-title: 自定义授权扩展
title: 自定义授权扩展
uuid: 588b05e5-3402-4586-bbd4-58b7e9a58ee4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 自定义授权扩展{#custom-authorization-extensions}

您可以在获取许可证期间调用自定义授权逻辑，以决定是否应将许可证颁发给请求客户端。

如果要实施您自己的客户授权扩展，您必须首先查看位于示例目 [!DNL SampleAuthorizer.java] 录中的示例代码。 此示例的编译版本位于 [!DNL flashaccess-license-server-ext-sample.jar]。

如果要构建自己的扩展，您需要实现接口，并确 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 保在构建路径中(如果在中使用某些字段， [!DNL flashaccess-license-server-exts.jar] 则还必须在构建路径中 [!DNL commons-logging.jar][!DNL adobe-flashaccess-sdk.jar]`IMessageFacade`)。

如果要部署扩展，您需要将jar或类文件复制到 *LicenseServer.ConfigRoot*[!DNL /flashaccessserver/libs]。

如果要更新jar或类文件，您需要在使用更新版本之前重新启动服务器。 您还必须将授权者类名称添加到租户配置文件。
