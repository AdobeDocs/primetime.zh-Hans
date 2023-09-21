---
title: 许可证服务器部署选项
description: 许可证服务器部署选项
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 许可证服务器部署选项{#license-server-deployment-options}

您可以使用以下选项之一来部署许可证服务器：

* 适用于受保护流的Adobe Primetime DRM服务器 — 此许可证服务器针对流进行了优化。 例如，您可以设置服务器以便使用Primetime DRMHTTP Dynamic StreamingAdobe。 此服务器部署简单，只需很少的配置，并且支持多个租户。 它能够实现高水平的可扩展性。 由于此实施针对流进行了优化，因此它不支持完整的Primetime DRM功能。 例如，不支持用户名/密码身份验证、域和许可证链接。 此服务器颁发的许可证中的使用规则通过服务器配置文件进行控制，该配置文件将覆盖打包时使用的策略。

  请参阅 *《 Adobe Primetime DRM Server for Protected Streaming指南》* 有关许可证服务器支持的使用规则的更多详细信息。
* 参考实施许可证服务器 — 您可以使用此设置来自定义您的服务器实施。 这是一个许可证服务器实施（包括源代码）示例，该示例演示了如何使用Primetime DRM SDK中的API来管理所有类型的请求，以及如何实施由数据库支持的自定义业务逻辑。 此服务器颁发的许可证中的使用规则通过打包时与内容关联的策略进行控制。
* 自定义服务器实施 — 您还可以使用SDK实施自己的许可服务器。 此信息描述如何使用API实施许可证服务器。
