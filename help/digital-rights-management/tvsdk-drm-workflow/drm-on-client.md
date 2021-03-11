---
title: Primetime DRM在客户端
description: Primetime DRM在客户端
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# 客户端上的Primetime DRM{#primetime-drm-on-the-client}

播放受保护内容的Primetime TVSDK应用程序必须首先调用Primetime DRM API，以启动许可证使用和受保护内容播放的工作流程。 在此工作流中，客户端上的Primetime DRM根据受保护内容的元数据构建许可证请求，然后将其发送到Primetime DRM许可证服务器。

在发出许可证请求之前，客户可以选择执行必要的身份验证/授权（取决于您的业务规则）。
