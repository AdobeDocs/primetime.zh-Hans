---
title: 典型工作流
description: 典型工作流
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 典型工作流{#typical-workflow}

这是一个典型的Primetime DRM参考实施工作流程，它同时具备命令行工具和许可证服务器功能：

1. 使用策略命令行工具创建DRM策略。
1. 使用Packager命令行工具加密内容。
1. 部署参考实现许可证服务器。
1. 将视频播放器上传到Web服务器。
1. 使用上传的视频播放器获取许可证并播放加密内容。

由于此典型工作流同时使用命令行工具和许可证服务器，因此您需要在继续之前安装和配置这两个组件。
