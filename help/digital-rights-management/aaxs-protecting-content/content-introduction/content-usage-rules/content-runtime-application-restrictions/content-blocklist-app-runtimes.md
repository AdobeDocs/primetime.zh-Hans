---
seo-title: 阻止限制访问受保护内容的应用程序运行时列表
title: 阻止限制访问受保护内容的应用程序运行时列表
uuid: 462a2c09-b335-4768-bd0e-1359db169d69
translation-type: tm+mt
source-git-commit: fbc175f383c850a7286b1e6e89daa027e00b29ef
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 阻止限制访问受保护内容的应用程序运行时列表 {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

指定无法访问内容的Primetime或Flash Runtime版本。 指定受限运行时（Flash Player、AIR或iOS）、平台和版本。

示例用例： 与DRM客户端块列表类似，最新版Flash Player、AIR或iOS运行时可指定为获取许可证和内容回放所需的最低版本。

除了以下属性外，应用程序运行时还可以由DRM客户端版本支持的任何属性进行标识：

| **属性** | **支持的值** | **匹配条件** | **说明** |
|---|---|---|---|
| 应用程序 | &quot;FlashPlayer&quot;、&quot;AIR&quot;、&quot;DRM_Library&quot;、&quot;AVE&quot; | 精确匹配 | 标识应用程序运行时的名称。 |

