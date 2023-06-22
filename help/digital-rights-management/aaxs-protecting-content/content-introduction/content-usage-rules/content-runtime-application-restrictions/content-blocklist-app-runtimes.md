---
title: 应用程序运行时阻止列表因访问受保护内容而受到限制
description: 应用程序运行时阻止列表因访问受保护内容而受到限制
copied-description: true
exl-id: 7c9d9e31-1a8d-4c76-9f2c-fcda58de1a42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 应用程序运行时阻止列表因访问受保护内容而受到限制 {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

指定无法访问内容的Primetime或Flash运行时的版本。 指定受限制的运行时(Flash Player、AIR或iOS)、平台和版本。

示例用例：与DRM客户端阻止列表类似，可将最新版本的Flash Player、AIR或iOS运行时指定为许可证获取和内容播放所需的最低版本。

除了以下属性外，还可以通过DRM客户端版本支持的任意属性来标识应用程序运行时：

| **属性** | **支持的值** | **匹配条件** | **描述** |
|---|---|---|---|
| 应用程序 | &quot;FlashPlayer&quot;、&quot;AIR&quot;、&quot;DRM_Library&quot;、&quot;AVE&quot; | 完全匹配 | 标识应用程序运行时的名称。 |
