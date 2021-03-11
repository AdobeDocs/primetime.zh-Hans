---
title: 带外许可证
description: 带外许可证
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 带外许可证{#out-of-band-licenses}

使用Primetime DRM，您可以实现一个客户在带外获得预生成许可证的工作流程，因此无需部署许可证服务器。 要支持此工作流，应在打包时指定一个选项，指示没有可用的许可证服务器。 这可防止客户端试图从许可证服务器请求此内容的许可证。

指示许可证服务器不可用的内容只能在Primetime DRM客户端版本3.0或更高版本上播放。 较旧的客户端需要升级才能播放此内容。
