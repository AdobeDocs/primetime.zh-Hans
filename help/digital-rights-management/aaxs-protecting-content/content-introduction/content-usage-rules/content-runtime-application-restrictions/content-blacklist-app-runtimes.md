---
seo-title: 限制访问受保护内容的应用程序运行时的黑名单
title: 限制访问受保护内容的应用程序运行时的黑名单
uuid: 462a2c09-b335-4768-bd0e-1359db169d69
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 限制访问受保护内容的应用程序运行时的黑名单 {#blacklist-of-application-runtimes-restricted-from-accessing-protected-content}

指定无法访问内容的Primetime或Flash Runtime版本。 指定受限运行时（Flash Player、AIR或iOS）、平台和版本。

示例用例：与DRM客户端黑名单相似，可以将Flash Player、AIR或iOS运行时的最新版本指定为获取许可证和内容播放所需的最低版本。

除了以下属性外，应用程序运行时还可以由DRM客户端版本支持的任何属性来标识：

| **属性** | **支持的值** | **匹配条件** | **说明** |
|---|---|---|---|
| 应用程序 | “FlashPlayer”、“AIR”、“DRM_Library”、“AVE” | 精确匹配 | 标识应用程序运行时的名称。 |

