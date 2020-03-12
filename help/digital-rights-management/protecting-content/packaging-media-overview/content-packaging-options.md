---
seo-title: 打包选项
title: 打包选项
uuid: 04244428-cb42-438a-8f16-91532c70ea60
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 打包选项{#packaging-options}

您可以使用许多选项来打包内容。 您可以在接口中指定 `DRMParameters` 选项并实现可接口的类。 通过这些类，您可以设置签名和密钥参数，并指示是加密音频内容、视频内容还是脚本数据。 要了解如何在参考实现中实现这些功能，请参阅使用Adobe Primetime DRM参考实施中讨论的Media Packager命 *令行选项的说明*。 这些选项基于Java API，因此可用于程序化使用。

打包选项包括：

* 加密选项（音频、视频、部分加密）。
* 客户端用作发送到许可证服务器的所有请求的基本URL的许可证服务器URL
* 许可证服务器传输证书
* 用于加密CEK的许可证服务器证书
* 用于对元数据进行签名的Packager凭据

