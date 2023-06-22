---
title: 使用DRM策略概述
description: 使用DRM策略概述
copied-description: true
exl-id: 734d0be3-2abe-400c-bc34-00046ec52f4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 概述 {#working-with-drm-policies-overview}

内容提供商可以使用Primetime DRM SDK将DRM策略应用于媒体文件。 然后，管理员可以使用策略管理API创建、查看详细信息和更新DRM策略。

A *`DRM policy`* 是包含安全设置、身份验证要求和使用权限的信息集合。 该策略定义用户查看内容的方式。 DRM策略、加密和签名允许内容提供商保持对其内容的控制，无论内容分发的范围有多广。

DRM策略用作许可证服务器在生成许可证时使用的模板。 客户端还可以在其请求许可证之前参考DRM策略，以确定客户端在向服务器发出许可证请求之前是否需要提示用户进行验证。

您可以使用AdobeFlash Media Server或HTTP服务器交付受保护的内容。 用户可在使用Primetime DRM SDK构建的自定义播放器中下载和播放受保护的内容。

DRM策略指定授予客户端的一个或多个权限。 通常，DRM策略至少包括 *`Play Right`*. 您还可以指定多个播放权限，每个权限具有不同的限制。 当客户端收到具有多个播放权限的许可证时，它会使用满足所有限制的第一个许可证。 例如，您可以在不同平台上实施不同的输出保护设置。

参见 `CreatePolicyWithOutputProtection.java` 在参考实施命令行工具中 [!DNL samples] 目录，以获取说明此示例的示例代码。

您可以使用Primetime DRM策略管理API完成以下任务：

* 创建和更新策略
* 查看DRM策略详细信息
* 管理DRM策略更新列表

请参阅 *Primetime DRM API参考* 以了解有关Java API的详细信息。

请参阅 *使用Primetime DRM参考实施* 有关Primetime DRM策略管理器的信息的指南。
