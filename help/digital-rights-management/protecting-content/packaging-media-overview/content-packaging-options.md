---
title: 打包选项
description: 打包选项
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# 打包选项{#packaging-options}

打包内容有多种选项。 您可以在中指定选项 `DRMParameters` 接口并实施可以接口的类。 使用这些类，您可以设置签名和密钥参数，以及指示是加密音频内容、视频内容还是脚本数据。 要了解如何在参考实施中实现这些功能，请参阅中讨论的Media Packager命令行选项的说明 *使用Adobe Primetime DRM参考实施*. 这些选项基于Java API，因此可用于编程。

打包选项包括：

* 加密选项（音频、视频、部分加密）。
* 客户端用作发送到许可证服务器的所有请求的基本URL的许可证服务器URL
* 许可证服务器传输证书
* 许可证服务器证书，用于加密CEK
* 用于签名元数据的打包程序凭据
