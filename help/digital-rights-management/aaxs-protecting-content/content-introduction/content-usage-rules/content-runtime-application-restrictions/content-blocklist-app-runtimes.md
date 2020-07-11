---
seo-title: 阻止列表应用程序运行时无法访问受保护的内容
title: 阻止列表应用程序运行时无法访问受保护的内容
uuid: 462a2c09-b335-4768-bd0e-1359db169d69
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 阻止列表应用程序运行时无法访问受保护的内容 {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

指定无法访问内容的Primetime或Flash Runtime版本。 指定受限运行时（Flash Player、AIR或iOS）、平台和版本。

示例用例： 与DRM客户端阻止列表相似，可将最新版Flash Player、AIR或iOS运行时指定为获取许可证和内容回放所需的最低版本。

除了以下属性外，应用程序运行时还可以由DRM客户端版本支持的任何属性进行标识：

| **属性** | **支持的值** | **匹配条件** | **说明** |
|---|---|---|---|
| 应用程序 | &quot;FlashPlayer&quot;、&quot;AIR&quot;、&quot;DRM_Library&quot;、&quot;AVE&quot; | 精确匹配 | 标识应用程序运行时的名称。 |
