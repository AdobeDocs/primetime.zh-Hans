---
description: 'null'
seo-description: 'null'
seo-title: 典型工作流
title: 典型工作流
uuid: aafe0030-8a59-4090-aeac-76867777eaa5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 典型工作流{#typical-workflow}

这是一个典型的Primetime DRM参考实现工作流程，它同时具有命令行工具和许可证服务器功能：

1. 使用策略命令行工具创建DRM策略。
1. 使用Packager命令行工具加密内容。
1. 部署参考实现许可证服务器。
1. 将视频播放器上传到Web服务器。
1. 使用上传的视频播放器获取许可证并播放加密内容。

由于此典型工作流同时使用命令行工具和许可证服务器，因此您需要在继续之前安装和配置这两个组件。
