---
title: 阻止列表应用程序运行时受限于访问受保护内容
description: 阻止列表应用程序运行时受限于访问受保护内容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 阻止列表应用程序运行时无法访问受保护的内容{#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

指定无法访问内容的Primetime或Flash Runtime版本。 指定受限运行时(Flash Player、AIR或iOS)、平台和版本。

示例用例：与DRM客户端阻止列表类似，最新版Flash Player、AIR或iOS运行时可指定为获取许可证和内容回放所需的最低版本。

除了以下属性外，应用程序运行时还可以由DRM客户端版本支持的任何属性进行标识：

| **属性** | **支持的值** | **匹配条件** | **说明** |
|---|---|---|---|
| 应用程序 | &quot;FlashPlayer&quot;、&quot;AIR&quot;、&quot;DRM_Library&quot;、&quot;AVE&quot; | 精确匹配 | 标识应用程序运行时的名称。 |
