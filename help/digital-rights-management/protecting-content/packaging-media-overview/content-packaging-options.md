---
title: 打包选项
description: 打包选项
copied-description: true
exl-id: 64c5c22d-0041-4fb9-80d0-72e11cb775f3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# 打包选项{#packaging-options}

打包内容有多种选项。 您可以在中指定选项 `DRMParameters` 接口并实现can接口的类。 使用这些类，您可以设置签名和密钥参数，以及指示是加密音频内容、视频内容还是脚本数据。 要了解如何在参考实施中实施这些选项，请参阅中讨论的“媒体打包程序”命令行选项的说明。 *使用Adobe Primetime DRM参考实施*. 这些选项基于Java API，因此可用于编程。

打包选项包括：

* 加密选项（音频、视频、部分加密）。
* 客户端用作发送到许可证服务器的所有请求的基本URL的许可证服务器URL
* 许可证服务器传输证书
* 许可证服务器证书，用于加密CEK
* 用于签名元数据的打包程序凭据
