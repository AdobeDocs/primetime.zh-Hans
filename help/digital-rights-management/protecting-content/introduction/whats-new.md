---
description: Adobe Primetime DRM是用于高价值视听内容的高级Digital Rights Management(DRM)和内容保护解决方案。 在支持创建Java API的应用程序中，您可以使用Primetime DRM SDK指定DRM策略，将这些策略应用于内容并加密该内容。
title: Adobe Primetime DRM的新增功能
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}的新增功能

Adobe Primetime DRM是用于高价值视听内容的高级Digital Rights Management(DRM)和内容保护解决方案。 在支持创建Java API的应用程序中，您可以使用Primetime DRM SDK指定DRM策略，将这些策略应用于内容并加密该内容。

>[!NOTE]
>
>Primetime DRM以前称为Adobe访问，在此之前称为Flash Access。

下面是内容保护流程的高级介绍：

1. 使用DRM Java API设置DRM策略属性和加密参数。
1. 创建描述任何内容的使用角色的DRM策略。

   您可以创建任意数量的DRM策略。 大多数用户创建少量策略，然后将其应用到多个文件。
1. 打包媒体文件。

   *`Packaging a file`* 表示您加密文件，然后对文件应用DRM策略。
1. 实施许可证服务器以向用户颁发许可证。

完成这些步骤后，您的加密内容便可供部署。 部署后，客户端可以从许可证服务器请求许可证，在收到后可以播放内容。

Primetime DRM SDK提供Java API以完成这些任务。 SDK包括许可证服务器和命令行工具的参考实现，这两者均基于DRM SDK Java API。

下面描述的功能是此版本中的新增功能。

## 新增功能{#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **硬停止 —** 您可以指定在播放窗口的末尾停止还是继续播放。
* **与分辨率相关的输出控** 件 — 您可以根据像素分辨率指定输出约束。
* **许可证服务器响应的匿名** 化 — 为了通过Primetime DRM许可证服务器协议增强隐私，传输证书序列号将被定位为许可证服务器对支持客户端的响应。

