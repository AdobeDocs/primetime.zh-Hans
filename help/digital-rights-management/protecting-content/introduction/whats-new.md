---
description: Adobe Primetime DRM是用于高价值视听内容的高级Digital Rights Management(DRM)和内容保护解决方案。 在支持创建Java API的应用程序中，您可以使用Primetime DRM SDK指定DRM策略、将这些策略应用于内容并对该内容进行加密。
title: Adobe Primetime DRM的新增功能
exl-id: 998dae80-b3d3-419e-8fd3-d925a83d8b53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Adobe Primetime DRM的新增功能{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM是用于高价值视听内容的高级Digital Rights Management(DRM)和内容保护解决方案。 在支持创建Java API的应用程序中，您可以使用Primetime DRM SDK指定DRM策略、将这些策略应用于内容并对该内容进行加密。

>[!NOTE]
>
>Primetime DRM以前称为Adobe访问，在此之前称为Flash Access。

下面是内容保护过程的高级演练：

1. 使用DRM Java API设置DRM策略属性和加密参数。
1. 创建描述任何内容的使用角色的DRM策略。

   您可以创建任意数量的DRM策略。 大多数用户会创建少量策略，然后将其应用于许多文件。
1. 打包媒体文件。

   *`Packaging a file`* 表示您先加密文件，然后将DRM策略应用到文件。
1. 实施许可证服务器以向用户颁发许可证。

完成这些步骤后，您的加密内容即可进行部署。 在部署之后，客户端可以从许可证服务器请求许可证，并且在接收到时可以播放内容。

Primetime DRM SDK提供了一个Java API来完成这些任务。 SDK包括许可证服务器和命令行工具的引用实施，两者都基于DRM SDK Java API。

下面介绍的功能是此版本中的新增功能。

## 新增功能 {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **硬停止 —** 您可以指定在播放窗口结束时是停止播放还是继续播放。
* **取决于分辨率的输出控件 —** 可根据像素分辨率指定输出约束。
* **许可证服务器响应的匿名化 —** 为了通过Primetime DRM许可证服务器协议增强隐私，传输证书序列号将清零，以便许可证服务器响应支持客户端。
