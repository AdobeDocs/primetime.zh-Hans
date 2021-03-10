---
title: 打包选项
description: 打包选项
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# 打包选项{#packaging-options}

您可以使用许多选项来打包内容。 可以在`DRMParameters`接口中指定选项，并实现可以接口的类。 通过这些类，您可以设置签名和密钥参数，并指示是加密音频内容、视频内容还是脚本数据。 要了解如何在参考实现中实现这些功能，请参阅&#x200B;*使用Adobe Primetime DRM参考实现*&#x200B;中讨论的Media Packager命令行选项说明。 这些选项基于Java API，因此可用于编程用途。

打包选项包括：

* 加密选项（音频、视频、部分加密）。
* 客户端用作发送到许可证服务器的所有请求的基本URL的许可证服务器URL
* 许可证服务器传输证书
* 用于加密CEK的许可证服务器证书
* 用于对元数据进行签名的打包程序凭据

