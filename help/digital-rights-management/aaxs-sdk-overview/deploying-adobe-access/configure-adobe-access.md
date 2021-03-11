---
title: 部署Adobe访问
description: 部署Adobe访问
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# 部署Adobe访问{#deploy-adobe-access}

Adobe Access SDK的一个关键优势是，您可以将它安装在任何Java™应用程序服务器或Servlet容器（如Tomcat）上。 您还需要JDK™ 1.5或更高版本。 有关软件要求的更多信息，请参阅Adobe Access SDK平台要求：[:https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/)。

部署Adobe访问的高级步骤有：

1. 安装和配置Adobe Access SDK。
1. 从Adobe获取数字证书。
1. 使用SDK创建许可证服务器，或部署Adobe Access Server以用于受保护流。
1. 创建内容打包和策略管理工具以打包内容、使用提供的内容准备工具或许可某个Adobe HTTP Dynamic Streaming打包程序。
1. 定义内容的使用规则，并创建支持这些规则的策略。
1. 使用打包和策略管理工具打包您的内容。
1. 开发视频应用程序，消费者可以使用Flash Player或Adobe AIR来视图您受保护的内容，或使用支持Adobe访问的已建立的OVP（在线视频平台）。
1. 将SWF文件部署到您的网站中以与Flash Player一起使用，或发布Adobe AIR安装程序进行下载。

这些步骤在以下几节中进行了扩展，并引用了包含其他信息的其他文档。

## 部署在64位操作系统{#deploying-on-a-bit-operating-system}上

64位操作系统，如64位版本的RedHat或Windows，与32位操作系统相比，其性能要好得多。

## 安装Adobe Access SDK {#install-adobe-access-sdk}

Adobe Access SDK以Java归档文件(JAR)文件的形式提供。 要了解有关安装Adobe Access的更多信息，请参阅&#x200B;*使用Adobe Access SDK保护内容*&#x200B;和&#x200B;*安全部署准则*。

## 实施许可证服务器{#implement-a-license-server}

使用Adobe Access SDK，您必须创建许可证服务器。 使用Adobe Access保护内容时，只有通过许可证服务器向消费者颁发许可证后，才能查看内容。 如果使用基于身份的许可，则基于密码的身份验证可确保只有经过授权的消费者才能打开和视图内容。

实施许可证服务器时，必须从Adobe获得必要的数字证书。 有关申请证书的详细说明，请参阅Adobe访问证书注册文档。

要了解有关实施许可证服务器和获取数字证书的更多信息，请参阅*使用Adobe Access SDK保护内容。*

## 创建内容打包和策略管理工具{#create-content-packaging-and-policy-management-tools}

使用Adobe Access SDK，您可以创建内容打包和策略管理工具。 策略管理API允许管理员创建、视图策略的详细信息和更新策略。 打包API将策略嵌入到FLV或F4V文件中，并使用内容加密密钥加密文件。

Adobe Access SDK包含一个引用实现([!DNL AdobePackager.jar])，它提供内容打包和策略管理工具([!DNL AdobePolicyManager.jar])的示例。

要了解有关创建内容打包和策略管理工具的更多信息，请参阅&#x200B;*使用Adobe Access SDK保护内容*。

## 创建策略和包内容{#create-policies-and-package-content}

使用SDK支持的使用规则，您必须定义和创建支持贵组织业务模型的策略，然后使用这些策略打包您的内容。 在打包期间对内容应用策略后，无论内容的分发范围有多广，您都可以保持对内容的控制。

Adobe Access中的策略支持各种不同的使用规则，包括：

* 指定消费者开始观看内容后许可证有效的天数。
* 允许许可证缓存。
* 指定可访问内容的客户端运行时和版本(例如，用户必须具有某个Adobe AIR应用程序或特定版本的Flash Player)。
* 要求消费者在查看受保护的内容或允许匿名访问之前使用用户名和密码进行身份验证。

要了解有关打包内容的更多信息，请参阅&#x200B;*保护内容*。 要了解有关使用规则及其支持的业务模型的更多信息，请参阅&#x200B;*使用规则*。

## 开发用于视频播放的应用程序{#develop-applications-for-video-playback}

要使消费者能够访问和视图内容，请使用Flash Player或Adobe AIR开发视频播放应用程序。 开发视频播放应用程序后，您必须将其部署到消费者。 如果您使用Flash Player开发应用程序，请将其托管在您组织的网站上。 如果您使用Adobe® AIR®开发应用程序，请发布AIR应用程序安装程序，以便消费者可以在其计算机上安装该应用程序。

要进一步了解如何开发与Adobe Access一起使用的自定义视频播放应用程序，请参阅[ActionScript 3.0开发人员指南](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)*、*[Adobe视频技术中心](https://www.adobe.com/devnet/video/)和Open Source Media Framework中的“使用视频”一章。