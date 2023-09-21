---
title: 部署Adobe Primetime DRM
description: 部署Adobe Primetime DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# 部署Adobe Primetime DRM {#configure-adobe-primetime-drm}

Adobe Primetime DRM SDK的主要优势在于，您可以将其安装在任何Java™应用程序服务器或Servlet容器（如Tomcat）上。 您还需要JDK™ 1.5或更高版本。 有关软件要求的更多信息，请参阅Primetime DRM SDK平台要求： [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

部署Primetime DRM的高级步骤包括：

1. 安装和配置Primetime DRM SDK。
1. 从Adobe获取数字证书。
1. 使用SDK创建许可证服务器，或部署Primetime DRM Server for Protected Streaming。
1. 创建内容打包和策略管理工具以打包内容，使用提供的内容准备工具，或许可某个AdobeHTTP Dynamic Streaming打包程序。
1. 为您的内容定义使用规则，并创建策略以支持这些规则。
1. 使用打包和策略管理工具打包您的内容。
1. 开发视频应用程序，让消费者可以使用Flash Player或Adobe AIR查看受保护的内容，或使用支持Primetime DRM的已建立的OVP（在线视频平台）。
1. 将用于Flash Player的SWF文件部署到您的网站，或者发布Adobe AIR安装程序以供下载。

这些步骤将在以下各节中展开，并会参考包含其他信息的其他文档。

## 在64位操作系统上部署{#deploying-on-a-bit-operating-system}

64位操作系统（如64位版本的RedHat或Windows）比32位操作系统提供更好的性能。

## 安装Adobe Primetime DRM SDK {#install-adobe-primetime-drm-sdk}

Primetime DRM SDK是作为Java存档(JAR)文件提供的。 要了解有关安装Primetime DRM的更多信息，请参阅使用Adobe Primetime DRM SDK保护内容和安全部署准则。

## 实施许可证服务器 {#implement-a-license-server}

使用Adobe Primetime DRM SDK时，您必须创建许可证服务器。 当使用Primetime DRM保护内容时，除非许可证服务器向消费者颁发许可证，否则无法查看内容。 如果使用基于身份的许可，则基于密码的身份验证可确保只有经过授权的用户才能打开和查看内容。

实施License Server时，必须从Adobe获取必要的数字证书。 有关请求证书的详细说明，请参阅Primetime DRM证书注册文档。

要了解有关实施许可证服务器和获取数字证书的更多信息，请参阅 **使用Adobe Primetime DRM SDK保护内容。**

## 创建内容打包和策略管理工具{#create-content-packaging-and-policy-management-tools}

使用Adobe Primetime DRM SDK，您可以创建内容打包和策略管理工具。 策略管理API允许管理员创建、查看策略详情以及更新策略。 打包API将策略嵌入到视频文件中，并使用内容加密密钥加密文件。

Primetime DRM SDK包括参考实施( [!DNL AdobePackager.jar])提供了内容打包和策略管理工具的示例( [!DNL AdobePolicyManager.jar])。

要了解有关创建内容打包和策略管理工具的更多信息，请参阅 **使用Adobe Primetime DRM SDK保护内容。**

## 创建策略和包内容 {#create-policies-and-package-content}

使用SDK支持的使用规则，您必须定义和创建策略以支持贵组织的业务模型，然后使用这些策略打包您的内容。 在打包过程中将策略应用于内容后，无论内容的分布范围有多广，您都可以保持对内容的控制。

Adobe Primetime DRM中的策略支持各种不同的使用规则，包括：

* 指定消费者开始观看内容后许可证的有效天数。
* 允许许可证缓存。
* 指定可以访问内容的客户端运行时和版本(例如，用户必须具有特定的Adobe AIR应用程序或Flash Player的特定版本)。
* 要求消费者在查看受保护内容之前使用用户名和密码进行身份验证，或者允许匿名访问。

要了解有关打包内容的更多信息，请参阅 *保护内容*. 要了解有关使用规则及其支持的业务模型的更多信息，请参阅 *使用规则*.

## 开发视频播放应用程序 {#develop-applications-for-video-playback}

要使使用者能够访问和查看内容，请使用Flash Player或Adobe AIR开发视频播放应用程序。 开发视频播放应用程序后，必须将其部署到使用者。 如果您使用Flash Player开发应用程序，请将其托管在您组织的网站上。 如果您使用Adobe® AIR®开发应用程序，请发布AIR应用程序安装程序，以便消费者可以下载该应用程序并将其安装在他们的计算机上。

要了解有关开发自定义视频播放应用程序以用于Adobe Primetime DRM的更多信息，请参阅中的“使用视频”一章 [《ActionScript 3.0开发人员指南》](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)， [Adobe视频技术中心](https://www.adobe.com/devnet/video/)和Open Source Media Framework。
