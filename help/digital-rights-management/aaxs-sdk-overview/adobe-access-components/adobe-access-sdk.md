---
description: Adobe访问的主要组件包括Java SDK以及Flash Player和Adobe AIR客户端运行时环境。
seo-description: Adobe访问的主要组件包括Java SDK以及Flash Player和Adobe AIR客户端运行时环境。
seo-title: Java SDK、Flash Player和Adobe AIR客户端
title: Java SDK、Flash Player和Adobe AIR客户端
uuid: 6b6c5aa2-56ee-4476-a05b-dcbbe3b9001e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# Adobe访问组件{#adobe-access-components}

Adobe访问的主要组件包括Java SDK以及Flash Player和Adobe AIR客户端运行时环境。

有关设置SDK的详细信息，请参阅&#x200B;*使用Adobe访问SDK保护内容中的设置SDK。*

Adobe访问SDK允许您开发与组织现有业务基础结构(如内容管理、计费和用户访问控制系统)集成的数字版权管理解决方案。 Flash Player和Adobe AIR使您能够创建和轻松部署应用程序，通过这些应用程序，消费者可以访问和视图大型数字内容库。

## Adobe访问SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe访问是作为Java SDK交付的，它提供可从中创建服务器实现的构件块。 使用SDK，您可以创建适合您组织的业务模型的Adobe访问解决方案。

SDK中提供的Java API在以下子部分中有介绍。

## 用于管理设备组域{#java-apis-for-managing-device-group-domains}的Java API

这些API用于允许服务器处理加入和离开设备组域的客户端请求。

设备组域是能够彼此共享许可证的设备的逻辑集合。 为了实现此目的，每个设备必须先加入／注册到同一域。 在服务器上运行的Adobe访问SDK必须处理设备域加入（注册）请求以及设备域离开（注销）请求。 未加入任何域的设备将获得绑定到该设备的许可证，该许可证不能共享到任何其他设备。

## 用于保护内容{#java-apis-for-protecting-content}的Java API

这些API用于定义权限和准备要分发的内容。 内容保护API包括：

* 策略管理

   策略管理API用于创建和修改要应用于内容的策略。 可以创建或更新策略，包括获取／设置所有使用规则以及允许自定义命名空间中的其他参数。

* 内容打包

   内容打包API用于加密内容并从打包内容中检索元数据。

## 用于颁发许可证的Java API {#java-apis-for-issuing-licenses}

当客户端从服务器请求许可证时，会使用这些API。 SDK支持来自客户端的以下请求：

* 身份验证

   身份验证API可用于处理身份验证请求和生成身份验证令牌。

* 许可证生成和获取

   许可证生成和获取API用于为用户生成许可证。

* 支持Adobe AIR版本1.5的客户端和内容

   为了向后兼容，SDK有API来处理来自AIR应用程序的请求，这些应用程序创建为与AIR版本1.5及更早版本的客户端及受保护的内容一起使用。

## 参考实现{#reference-implementation}

SDK包括一个参考实现，一个简单的Adobe访问部署，它演示了如何使用Java API。 该参考实现提供了License Server、Watched Folder Packager、Adobe访问管理器AIR应用程序和命令行工具，用于基于Java API的内容打包和策略管理。 要进一步了解Adobe访问参考实现，请参阅&#x200B;*保护内容*。

## Adobe Access Server保护流{#adobe-access-server-for-protected-streaming}

对于使用Adobe访问保护内容的流用例，如AdobeHTTP Dynamic Streaming，软件还包含Adobe Access Server的受保护流。 此解决方案可以轻松地部署在Servlet容器（如Tomcat）上，并可实现高级可伸缩性和性能，以满足最大的内容分发需求。

## AdobeFlash Player{#adobe-flash-player}

Flash Player是一款轻量级浏览器插件和运行时，可提供一致、引人入胜的用户体验、令人赞叹的音频／视频播放以及广泛的应用。 Flash Player为流式或下载的视频内容提供高质量回放。 对于内容发布者，Flash Player提供了自定义围绕内容的播放屏幕的方法，允许使用横幅和叠加通过广告实现更深层的品牌体验和货币化。 对于消费者而言，Flash Player提供了一种直观且具有视觉吸引力的视频内容视图方式。

有关Flash Player的更多信息，请访问：[www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR{#adobe-air}

Adobe AIR是一个跨操作系统运行时，它允许内容制作者通过设计自定义多媒体应用程序将他们在web上的现有投资扩展到桌面。 它以久经考验的开放式技术为构建和部署定制应用程序提供了一种可靠、简化的方式，这些应用程序可以被信任来提供更安全、更愉悦的用户体验。 Adobe AIR使企业能够轻松集成富媒体，创造更引人入胜的交互式用户体验。 它使开发人员能使用熟悉的工具(如HTML、JavaScript、Flash或Adobe®Flex®软件)将他们独特的富Internet应用程序组合部署到Windows、Macintosh或Linux。

企业可以完全控制用户界面，并可以设计用户体验来反映和强化其品牌。 借助对回放使用Adobe访问SDK保护的内容的内置支持，Adobe AIR帮助创建自定义的端到端内容分发链。

有关Adobe AIR的更多信息，请访问：[www.adobe.com/go/air](https://www.adobe.com/go/air)

## 本机iOS和Android应用程序{#native-ios-and-android-applications}

本机iOS和Android应用程序仅对Adobe Primetime客户可用，Adobe访问DRM 4.0及更高版本可用于保护移动设备上的本机(非Flash)应用程序内消耗的视频。 要使应用程序使用此受保护的内容，必须使用Adobe Primetime客户端库实现它。

有关Adobe Primetime的更多信息，请访问：[https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)