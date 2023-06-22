---
title: 应用程序运行时阻止列表
description: 应用程序运行时阻止列表
copied-description: true
exl-id: f8d1d385-41d4-4361-82c1-417b2ff421c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 应用程序运行时阻止列表 {#blocklist-of-application-runtimes}

应用程序运行时阻止列表指定无法访问内容的Primetime客户端或Flash运行时的版本。 指定受限制的运行时(Flash Player、AIR或iOS)、平台和版本。

示例用例：与Primetime DRM客户端阻止列表类似，可以将最新版本的Flash Player、AIR或iOS运行时指定为许可证获取和内容播放所需的最低版本。

除了以下属性外，还可以通过Primetime DRM客户端版本支持的任何属性来标识应用程序运行时：

| **属性** | **支持的值** | **匹配条件** | **描述** |
|---|---|---|---|
| 应用程序 | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | 完全匹配 | 标识应用程序运行时的名称。 |
