---
seo-title: 客户端上的Primetime DRM
title: 客户端上的Primetime DRM
uuid: 472180ad-6596-4a24-aa51-7909a75a5e10
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# 客户端上的Primetime DRM{#primetime-drm-on-the-client}

播放受保护内容的Primetime TVSDK应用程序必须首先调用Primetime DRM API，以启动许可证使用和受保护内容回放的工作流。 在此工作流中，客户端上的Primetime DRM根据受保护内容的元数据构建许可证请求，然后将其发送到Primetime DRM许可证服务器。

在发出许可证请求之前，客户端可以选择执行必要的身份验证／授权（取决于您的业务规则）。
