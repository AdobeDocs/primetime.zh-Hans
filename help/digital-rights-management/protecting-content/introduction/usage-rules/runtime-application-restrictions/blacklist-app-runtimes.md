---
description: 'null'
seo-description: 'null'
seo-title: 应用程序运行时黑名单
title: 应用程序运行时黑名单
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 应用程序运行时黑名单{#blacklist-of-application-runtimes}

应用程序运行时的黑名单指定无法访问内容的Primetime客户端或Flash Runtime版本。 指定受限运行时（Flash Player、AIR或iOS）、平台和版本。

示例用例：与Primetime DRM客户端黑名单相似，最新版Flash Player、AIR或iOS运行时可指定为获取许可证和内容播放所需的最低版本。

除了以下属性外，您还可以通过Primetime DRM客户端版本支持的任何属性来标识应用程序运行时：

| **属性** | **支持的值** | **匹配条件** | **说明** |
|---|---|---|---|
| 应用程序 | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | 精确匹配 | 标识应用程序运行时的名称。 |

