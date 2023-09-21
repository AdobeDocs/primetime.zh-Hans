---
title: 概述
description: 概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 概述  {#overview}

使用Adobe®访问™，内容提供商可以将策略应用到媒体文件。 通过使用策略管理API，管理员可以创建、查看策略详情以及更新策略。

A *策略* 定义用户查看内容的方式；它是包含安全设置、身份验证要求和使用权限的信息集合。 在应用策略时，加密和签名允许内容提供商保持对其内容的控制，无论其内容分布得多广。 受保护的文件可以使用Adobe®Flash®Media Server或HTTP服务器交付。 它们可以在使用Adobe® AIR®、Adobe®Flash®播放器和Adobe® Primetime SDK for iOS构建的自定义播放器中下载和播放。 该策略是许可证服务器在生成许可证时使用的模板。 客户端也可以在请求许可证之前参考策略，以确定在向服务器发出许可证请求之前它是否需要提示用户进行身份验证。

策略指定授予客户端的一个或多个权限。 通常，策略至少包括“向右播放”。 也可以指定多个播放权限，每个权限具有不同的限制。 当客户端遇到具有多个播放权限的许可证时，它会使用满足所有限制的第一个许可证。 例如，此功能可用于在不同的平台上实施不同的输出保护设置。 有关说明此示例的示例代码，请参阅 `CreatePolicyWithOutputProtection.java` 在参考实施命令行工具“samples”目录中。

您可以使用策略管理API完成以下任务：

* 创建和更新策略
* 查看策略详细信息
* 管理策略更新列表

有关本章讨论的Java API的详细信息，请参阅 *Adobe访问API参考*.

有关Policy Manager参考实施的信息，请参见 *使用Adobe访问引用实施*.
