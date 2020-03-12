---
seo-title: 使用DRM策略概述
title: 使用DRM策略概述
uuid: 32423448-013c-4183-bea8-e14b6690abdb
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 概述 {#working-with-drm-policies-overview}

内容提供商可以使用Primetime DRM SDK将DRM策略应用到媒体文件。 然后，管理员可以使用策略管理API创建、查看DRM策略的详细信息和更新DRM策略。

A是 *`DRM policy`* 包含安全性设置、身份验证要求和使用权限的信息集合。 策略定义用户如何查看内容。 DRM策略、加密和签名允许内容提供商保持对其内容的控制，无论内容分发的范围有多广。

DRM策略用作许可证服务器在生成许可证时使用的模板。 客户端在请求许可证之前也可以参考DRM策略，以确定客户端在向服务器发出许可证请求之前是否需要提示用户进行身份验证。

您可以使用Adobe Flash Media Server或HTTP服务器交付受保护的内容。 用户可以在使用Primetime DRM SDK构建的自定义播放器中下载和播放受保护的内容。

DRM策略指定授予客户端的一个或多个权限。 通常，DRM策略至少包括 *`Play Right`*。 您还可以指定多个播放权限，每个权限具有不同的限制。 当客户端收到具有多个播放权限的许可证时，它使用第一个满足所有限制的许可证。 例如，您可以在不同平台上强制使用不同的输出保护设置。

有关 `CreatePolicyWithOutputProtection.java` 此示例的示例代码，请参 [!DNL samples] 阅Reference Implementation Command Line Tools目录中的示例代码。

您可以使用Primetime DRM策略管理API完成以下任务：

* 创建和更新策略
* 查看DRM策略详细信息
* 管理DRM策略更新列表

有关Java API *的详细信息* ，请参阅Primetime DRM API参考。

有关Primetime DRM *策略管理器的信息，请参阅* 《使用Primetime DRM参考实施指南》。
