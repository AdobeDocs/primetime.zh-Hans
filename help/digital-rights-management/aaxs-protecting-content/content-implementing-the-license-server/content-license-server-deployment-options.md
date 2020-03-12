---
seo-title: 许可证服务器部署选项
title: 许可证服务器部署选项
uuid: 297c587f-23e2-4bb5-911b-72d7b82370f4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 许可证服务器部署选项{#license-server-deployment-options}

可以使用以下任一选项部署许可证服务器：

* **Adobe Access Server for Protected Streaming** —此许可证服务器针对流进行了优化。 例如，您可以使用Adobe Access为Adobe HTTP动态流化设置服务器。 该服务器可以轻松部署，只需要很少的配置，并将支持多个租户，并可实现高级的可扩展性。 但是，由于此实施针对流进行了优化，因此它不支持完整的Adobe Access功能。 例如，用户名／密码身份验证、域和许可证链接不受支持。 此服务器所颁发的许可证中的使用规则通过服务器配置文件进行控制，该文件将覆盖打包时使用的策略。 有关此服 *务器支持的使用规则的详细信息* ，请参阅Adobe Access Server for Protected Streaming Guide。
* **参考实施许可证服务器** —将此设置用作自定义服务器实施的起点。 这是一个示例许可证服务器实施，包括源代码，它演示了如何使用Adobe Access SDK中的API处理所有类型的请求以及如何实现由数据库支持的自定义业务逻辑。 此服务器所颁发的许可证中的使用规则通过与打包时的内容相关联的策略进行控制。
* **自定义服务器实施** -您还可以使用SDK实施您自己的许可服务器。 本章中的信息描述了用于实现许可证服务器的API。

