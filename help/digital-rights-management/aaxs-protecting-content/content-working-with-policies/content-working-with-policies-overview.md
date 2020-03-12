---
seo-title: 概述
title: 概述
uuid: 7363d241-6947-4a9c-80e5-e50be71066b9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 概述 {#overview}

使用Adobe® Access™，内容提供商可以将策略应用于媒体文件。 使用策略管理API，管理员可以创建、查看策略的详细信息和更新策略。

策 *略定义* ，用户如何查看内容；它是包含安全设置、身份验证要求和使用权限的信息集合。 当应用策略时，加密和签名允许内容提供商保持对其内容的控制，而无论其分发范围有多广。 使用Adobe® Flash® Media Server或HTTP服务器可以交付受保护的文件。 可在使用Adobe® AIR®、Adobe® Flash® Player和Adobe® Primetime SDK for iOS构建的自定义播放器中下载和播放它们。 策略是许可证服务器在生成许可证时使用的模板。 客户端还可以在请求许可证之前参考该策略以确定它是否需要在向服务器发出许可证请求之前提示用户进行身份验证。

策略指定授予客户端的一个或多个权限。 通常，策略至少包括“播放权”。 还可以指定多个播放权限，每个播放权限具有不同的限制。 当客户端遇到具有多个播放权限的许可证时，它使用第一个满足所有限制的许可证。 例如，此功能可用于在不同平台上实施不同的输出保护设置。 有关说明此示例的示例代码，请参 `CreatePolicyWithOutputProtection.java` 阅Reference Implementation命令行工具“samples”目录中的示例。

您可以使用策略管理API完成以下任务：

* 创建和更新策略
* 查看策略详细信息
* 管理策略更新列表

有关本章中讨论的Java API的详细信息，请参 *阅Adobe Access API参考*。

有关策略管理器参考实施的信息，请参 *阅使用Adobe Access参考实施*。
