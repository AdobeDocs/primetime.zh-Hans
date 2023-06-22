---
title: 典型工作流程
description: 典型工作流程
copied-description: true
exl-id: c2020b48-7e97-4df5-a453-7b76e2e1d458
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 典型工作流程{#typical-workflow}

这是一个典型的Primetime DRM参考实施工作流，该工作流同时具有命令行工具和许可证服务器：

1. 使用策略命令行工具创建DRM策略。
1. 使用Packager命令行工具加密内容。
1. 部署参考实施许可证服务器。
1. 将视频播放器上传到Web服务器。
1. 使用上传的视频播放器获取许可证并播放加密的内容。

由于此典型工作流同时使用命令行工具和许可证服务器，因此您需要在继续操作之前安装和配置这两个组件。
