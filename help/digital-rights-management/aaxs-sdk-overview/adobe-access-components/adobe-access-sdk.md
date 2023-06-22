---
description: Adobe访问的主要组件包括Java SDK、Flash Player和Adobe AIR客户端运行时环境。
title: Java SDK、Flash Player和Adobe AIR客户端
exl-id: 2df4da13-8df9-442b-8638-317c41d62fbe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Adobe访问组件{#adobe-access-components}

Adobe访问的主要组件包括Java SDK、Flash Player和Adobe AIR客户端运行时环境。

有关设置SDK的更多信息，请参阅中的设置SDK 。 *使用Adobe访问SDK保护内容。*

Adobe访问SDK允许您开发数字权限管理解决方案，该解决方案与您组织的现有业务基础架构集成，例如内容管理、计费和用户访问控制系统。 通过Flash Player和Adobe AIR，您可以创建并轻松部署应用程序，消费者可以通过这些应用程序访问和查看大型数字内容库。

## Adobe访问SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe访问是以Java SDK的形式提供的，该SDK提供了构建块，您可以从中创建服务器实施。 使用SDK，您可以创建适合您组织业务模式的Adobe访问解决方案。

以下子部分介绍了在SDK中提供的Java API。

## 用于管理设备组域的Java API {#java-apis-for-managing-device-group-domains}

这些API用于允许服务器处理加入和离开设备组域的客户端请求。

设备组域是能够相互共享许可证的设备的一个逻辑集合。 为了做到这一点，每个设备必须首先联接/注册到同一个域。 在服务器上运行的Adobe访问SDK必须处理Device Domain join (register)请求以及Device Domain leave (de-register)请求。 对于未加入任何域的设备，将颁发绑定到该设备的许可证，该许可证不能共享到任何其他设备。

## 用于保护内容的Java API {#java-apis-for-protecting-content}

这些API用于定义权限并准备内容以进行分发。 内容保护API包括：

* 策略管理

   策略管理API用于创建和修改要应用于内容的策略。 可以创建或更新策略，包括获取/设置所有使用规则，以及允许在自定义命名空间中使用其他参数。

* 内容打包

   内容打包API用于加密内容并从打包的内容中检索元数据。

## 用于颁发许可证的Java API {#java-apis-for-issuing-licenses}

当客户端从服务器请求许可证时，将使用这些API。 SDK支持来自客户端的以下请求：

* 身份验证

   身份验证API可用于处理身份验证请求和生成身份验证令牌。

* 许可证生成和获取

   许可证生成和获取API用于为用户生成许可证。

* 支持Adobe AIR版本1.5客户端和内容

   为了向后兼容，SDK具有API以处理来自AIR应用程序的请求，这些应用程序是为与AIR版本1.5及更早版本的客户端及受保护内容一起使用而创建的。

## 参考实施 {#reference-implementation}

该SDK包含一个参考实施，以及一个演示如何使用Java API的简单Adobe访问部署。 参考实施提供了许可证服务器、Watched Folder Packager、Adobe访问管理器AIR应用程序和命令行工具，用于基于Java API的内容打包和策略管理。 要了解有关Adobe访问引用实施的更多信息，请参阅 *保护内容*.

## 适用于受保护流的Adobe Access Server {#adobe-access-server-for-protected-streaming}

对于使用Adobe访问保护内容的流用例(例如，AdobeHTTP Dynamic Streaming)，软件还包括适用于受保护流的Adobe Access Server。 此解决方案可以轻松地部署在Tomcat等servlet容器上，并且可以实现高级别的可扩展性和性能，以满足最大的内容分发需求。

## AdobeFlash Player {#adobe-flash-player}

Flash Player是一个轻量级的浏览器插件和运行时，可提供一致且引人入胜的用户体验、令人惊叹的音频/视频播放和广泛的访问范围。 Flash Player提供高质量播放流式传输或下载的视频内容。 对于内容发布者而言，Flash Player提供了自定义内容周围的播放屏幕的方法，从而允许通过使用横幅和覆盖图的广告实现更深入的品牌推广体验和盈利。 对于消费者而言，Flash Player提供了一种直观且美观的方式来查看视频内容。

有关Flash Player的详细信息，请访问： [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR是一个跨操作系统的运行时，它允许内容制作者通过设计自定义的多媒体应用程序将其在Web上的现有投资扩展到桌面。 它构建于经验证的开放式技术之上，为企业开发和部署可信的自定义应用程序提供了可靠、简化的方式，从而提供更安全、更愉快的用户体验。 Adobe AIR允许企业轻松集成富媒体，以创建更沉浸式和交互式的用户体验。 它使开发人员可以使用熟悉的工具(如HTML、JavaScript、Flash或Adobe®Flex®软件)将其独特的富互联网应用程序组合部署到Windows、Macintosh或Linux。

企业可以完全控制用户界面，并且可以设计用户体验来反映和加强其品牌。 Adobe AIR内置了对受Adobe访问SDK保护的内容播放的支持，可帮助创建自定义的端到端内容分发链。

有关Adobe AIR的更多信息，请访问： [www.adobe.com/go/air](https://www.adobe.com/go/air)

## 本机iOS和Android应用程序 {#native-ios-and-android-applications}

本机iOS和Android应用程序仅适用于Adobe Primetime客户，Adobe访问DRM 4.0及更高版本可用于保护在移动设备上本机(非Flash)应用程序中使用的视频。 要使应用程序使用此受保护的内容，必须使用Adobe Primetime客户端库实施它。

有关Adobe Primetime的更多信息，请访问： [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)
