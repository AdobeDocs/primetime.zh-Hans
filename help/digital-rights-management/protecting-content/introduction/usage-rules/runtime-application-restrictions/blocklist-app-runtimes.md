---
title: 阻止列表应用程序运行时
description: 阻止列表应用程序运行时
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 阻止列表应用程序运行时{#blocklist-of-application-runtimes}

阻止列表应用程序运行时指定无法访问内容的Primetime客户端或Flash运行时版本。 指定受限运行时(Flash Player、AIR或iOS)、平台和版本。

示例用例：与Primetime DRM客户端阻止列表类似，最新版的Flash Player、AIR或iOS运行时可指定为获取许可证和内容回放所需的最低版本。

除了以下属性外，您还可以通过Primetime DRM客户端版本支持的任何属性来标识应用程序运行时：

| **属性** | **支持的值** | **匹配条件** | **说明** |
|---|---|---|---|
| 应用程序 | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | 精确匹配 | 标识应用程序运行时的名称。 |

