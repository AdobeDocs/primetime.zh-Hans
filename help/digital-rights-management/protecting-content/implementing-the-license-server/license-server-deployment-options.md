---
seo-title: 许可证服务器部署选项
title: 许可证服务器部署选项
uuid: 732b948f-8037-423e-9f85-770d6316cbae
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 许可证服务器部署选项{#license-server-deployment-options}

您可以使用以下任一选项部署许可证服务器：

* 用于受保护流的Adobe Primetime DRM Server —— 此许可证服务器针对流进行了优化。 例如，您可以使用Primetime DRM为Adobe HTTP动态流设置服务器。 此服务器可以轻松部署，并且所需的配置很少，并支持多个租户。 它可以实现高级别的可伸缩性。 由于此实施针对流进行了优化，因此它不支持Primetime DRM的全部功能。 例如，用户名／密码身份验证、域和许可证链接不受支持。 此服务器所颁发的许可证中的使用规则通过服务器配置文件进行控制，该文件将覆盖打包时使用的策略。

   有关许可 *证服务器支持的使用规则的详细信息* ，请参阅Adobe Primetime DRM Server for Protected Streaming Guide。
* 参考实施许可证服务器——您可以使用此设置自定义您的服务器实施。 这是一个示例许可证服务器实施，包括源代码，它演示了如何使用Primetime DRM SDK中的API管理所有类型的请求以及如何实现由数据库支持的自定义业务逻辑。 此服务器所颁发的许可证中的使用规则通过与打包时的内容相关联的策略进行控制。
* 自定义服务器实施——您还可以使用SDK实施您自己的许可服务器。 该信息描述了如何使用API实施许可证服务器。

