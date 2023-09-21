---
title: 许可证服务器部署选项
description: 许可证服务器部署选项
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 许可证服务器部署选项{#license-server-deployment-options}

可以使用以下选项之一部署许可证服务器：

* **适用于受保护流的Adobe Access Server**  — 此许可证服务器针对流进行了优化。 例如，您可以设置服务器以使用Adobe访问权限进行AdobeHTTP Dynamic Streaming。 此服务器部署简单，只需要很少的配置，支持多个租户，并且能够实现高级别的可扩展性。 但是，由于此实施针对流进行了优化，因此它不支持完整的Adobe访问功能。 例如，不支持用户名/密码身份验证、域和许可证链接。 此服务器颁发的许可证中的使用规则通过服务器配置文件进行控制，该配置文件将覆盖打包时使用的策略。 请参阅 *Adobe Access Server for Protected Streaming指南* 有关此服务器支持的使用规则的更多详细信息。
* **参考实施许可证服务器**  — 使用此设置作为自定义服务器实施的起点。 这是一个许可证服务器实现（包括源代码）示例，该示例演示了如何使用Adobe访问SDK中的API处理所有类型的请求，以及如何实施由数据库支持的自定义业务逻辑。 此服务器颁发的许可证中的使用规则通过打包时与内容关联的策略进行控制。
* **自定义服务器实施**  — 您还可以使用SDK实施自己的许可服务器。 本章中的信息介绍用于实施许可证服务器的API。
