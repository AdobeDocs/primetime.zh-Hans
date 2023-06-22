---
title: 客户端上的Primetime DRM
description: 客户端上的Primetime DRM
copied-description: true
exl-id: 157d558f-3014-4d05-bba1-e73134cedc23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 客户端上的Primetime DRM{#primetime-drm-on-the-client}

播放受保护内容的Primetime TVSDK应用程序必须首先调用Primetime DRM API以启动许可证消耗和受保护内容播放的工作流。 在此工作流中，客户端上的Primetime DRM从受保护内容的元数据构造许可证请求，然后将其发送到Primetime DRM许可证服务器。

在发出许可证请求之前，客户端可以选择执行必要的身份验证/授权（具体取决于您的业务规则）。
