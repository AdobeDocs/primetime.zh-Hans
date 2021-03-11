---
title: 概述
description: 概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# 概述{#overview}

使用Adobe® Access™，内容提供商可以将策略应用于媒体文件。 使用策略管理API，管理员可以创建、视图策略的详细信息和更新策略。

*policy*&#x200B;定义用户如何视图内容；它是包含安全性设置、身份验证要求和使用权限的信息集合。 当应用策略时，加密和签名允许内容提供商保持对其内容的控制，无论内容分发的范围有多广。 可以使用Adobe® Flash® Media Server或HTTP服务器交付受保护的文件。 可在使用Adobe® AIR®、Adobe® Flash® Player和Adobe® Primetime SDK for iOS构建的自定义播放器中下载和播放它们。 策略是许可证服务器在生成许可证时使用的模板。 客户端还可以在请求许可证之前参考该策略，以确定它是否需要在向服务器发出许可证请求之前提示用户进行身份验证。

策略指定授予客户端的一个或多个权限。 通常，策略至少包括“播放权”。 还可以指定多个播放权限，每个播放权限具有不同的限制。 当客户遇到具有多个播放权限的许可证时，会使用第一个满足所有限制的许可证。 例如，此功能可用于在不同平台上实施不同的输出保护设置。 有关说明此示例的示例代码，请参阅Reference Implementation Command Line Tools &quot;samples&quot;目录中的`CreatePolicyWithOutputProtection.java`。

您可以使用策略管理API完成以下任务:

* 创建和更新策略
* 视图策略详细信息
* 管理策略更新列表

有关本章中讨论的Java API的详细信息，请参阅&#x200B;*Adobe访问API参考*。

有关策略管理器引用实现的信息，请参阅&#x200B;*使用Adobe访问引用实现*。
