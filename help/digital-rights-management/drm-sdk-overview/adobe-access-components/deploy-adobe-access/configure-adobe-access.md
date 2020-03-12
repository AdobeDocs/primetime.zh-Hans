---
seo-title: 部署Adobe Primetime DRM
title: 部署Adobe Primetime DRM
uuid: c14c2792-d207-4f39-b856-610520bdaa28
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# 部署Adobe Primetime DRM {#configure-adobe-primetime-drm}

Adobe Primetime DRM SDK的一个主要优势是，您可以将它安装在任何Java™应用程序服务器或servlet容器（如Tomcat）上。 您还需要JDK™ 1.5或更高版本。 有关软件要求的更多信息，请参阅Primetime DRM SDK平台要求： [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/)。

部署Primetime DRM的高级步骤包括：

1. 安装和配置Primetime DRM SDK。
1. 从Adobe获得数字证书。
1. 使用SDK创建许可证服务器，或部署Primetime DRM Server，以实现受保护的流。
1. 创建内容打包和策略管理工具以打包内容、使用提供的内容准备工具或许可其中一个Adobe HTTP Dynamic Streaming Packager。
1. 为您的内容定义使用规则，并创建支持这些规则的策略。
1. 使用打包和策略管理工具打包您的内容。
1. 开发视频应用程序，消费者可以使用它们使用Flash Player或Adobe AIR查看您的受保护内容，或使用支持Primetime DRM的已建立的OVP（在线视频平台）。
1. 将SWF文件部署到您的网站以与Flash Player一起使用，或发布Adobe AIR安装程序进行下载。

这些步骤在以下几节中进行了扩展，其中引用了包含其他信息的其他文档。

## 部署在64位操作系统上{#deploying-on-a-bit-operating-system}

64位操作系统（如64位版本的RedHat或Windows）比32位操作系统提供更好的性能。

## 安装Adobe Primetime DRM SDK {#install-adobe-primetime-drm-sdk}

Primetime DRM SDK以Java存档(JAR)文件的形式提供。 要了解有关安装Primetime DRM的更多信息，请参阅使用Adobe Primetime DRM SDK保护内容和安全部署指南。

## 实施许可证服务器 {#implement-a-license-server}

使用Adobe Primetime DRM SDK，您必须创建许可证服务器。 使用Primetime DRM保护内容时，只有在许可服务器向消费者颁发许可证后，才能查看该内容。 如果使用基于身份的许可，则基于密码的身份验证可确保只有经过授权的消费者才能打开和查看内容。

实施许可证服务器时，您必须从Adobe获得必要的数字证书。 有关申请证书的详细说明，请参阅Primetime DRM证书登记文档。

要进一步了解如何实施许可证服务器和获取数字证书，请参 **阅使用Adobe Primetime DRM SDK for Protecting Content。**

## 创建内容打包和策略管理工具{#create-content-packaging-and-policy-management-tools}

使用Adobe Primetime DRM SDK，您可以创建内容打包和策略管理工具。 策略管理API允许管理员创建、查看策略的详细信息和更新策略。 打包API将策略嵌入到视频文件中，并使用内容加密密钥加密文件。

Primetime DRM SDK包括参考实施( [!DNL AdobePackager.jar])，它提供内容打包和策略管理工具( [!DNL AdobePolicyManager.jar])的示例。

要了解有关创建内容打包和策略管理工具的更多信息，请 **参阅使用Adobe Primetime DRM SDK For Protecting Content。**

## 创建策略和包内容 {#create-policies-and-package-content}

使用SDK支持的使用规则，您必须定义和创建支持贵组织业务模型的策略，然后使用这些策略打包您的内容。 在打包期间对内容应用策略后，无论内容的分发范围有多广，您都可以对内容进行控制。

Adobe Primetime DRM中的策略支持各种不同的使用规则，包括：

* 指定在消费者开始观看内容后许可证有效的天数。
* 允许许可证缓存。
* 指定可访问内容的客户端运行时和版本（例如，用户必须拥有某个Adobe AIR应用程序或特定版本的Flash Player）。
* 要求消费者在查看受保护的内容或允许匿名访问之前使用用户名和密码进行身份验证。

要了解有关打包内容的更多信息，请参 *阅保护内容*。 要进一步了解使用规则及其支持的业务模型，请参阅使 *用规则*。

## 开发视频回放应用程序 {#develop-applications-for-video-playback}

要使消费者能够访问和查看内容，请使用Flash Player或Adobe AIR开发视频播放应用程序。 开发视频播放应用程序后，您必须将其部署到消费者。 如果您使用Flash Player开发应用程序，请将其托管在您组织的网站上。 如果您使用Adobe® AIR®开发应用程序，请发布AIR应用程序安装程序，以便消费者可以下载应用程序并将其安装到他们的计算机上。

要进一步了解如何开发与Adobe Primetime DRM一起使用的自定义视频播放应用程序，请参阅 [ActionScript 3.0开发人员指南中的“使用视频”一章](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)、 [Adobe视频技术中心](https://www.adobe.com/devnet/video/)，以及开放源媒体框架。