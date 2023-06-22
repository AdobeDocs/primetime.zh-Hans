---
description: Primetime DRM的主要组件包括Java SDK、Flash Player和Adobe AIR客户端运行时环境。
title: Java SDK、Flash Player和Adobe AIR客户端
exl-id: 5422d282-da9c-4810-a782-3c3af5fdeb3f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# ADOBE PRIMETIME DRM SDK {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM是以Java SDK的形式提供的，该SDK提供了构建块，您可以从中创建服务器实施。 使用SDK，您可以创建适合您组织业务模式的Primetime DRM解决方案。

以下子部分介绍了在SDK中提供的Java API。

## 用于管理设备组域的Java API{#java-apis-for-managing-device-group-domains}

这些API用于允许服务器处理加入和离开设备组域的客户端请求。

设备组域是能够相互共享许可证的设备的一个逻辑集合。 为了做到这一点，每个设备必须首先联接/注册到同一个域。 在服务器上运行的Primetime DRM SDK必须处理设备域加入（注册）请求以及设备域退出（注销）请求。 对于未加入任何域的设备，将颁发绑定到该设备的许可证，该许可证不能共享到任何其他设备。

## 用于保护内容的Java API{#java-apis-for-protecting-content}

这些API用于定义权限并准备内容以进行分发。 内容保护API包括：

* 策略管理

   策略管理API用于创建和修改要应用于内容的策略。 可以创建或更新策略，包括获取/设置所有使用规则，以及允许在自定义命名空间中使用其他参数。

* 内容打包

   内容打包API用于加密内容并从打包的内容中检索元数据。

## 用于颁发许可证的Java API{#java-apis-for-issuing-licenses}

当客户端从服务器请求许可证时，将使用这些API。 SDK支持来自客户端的以下请求：

* 身份验证

   身份验证API可用于处理身份验证请求和生成身份验证令牌。

* 许可证生成和获取

   许可证生成和获取API用于为用户生成许可证。

* 支持Adobe AIR版本1.5客户端和内容

   为了向后兼容，SDK具有API以处理来自AIR应用程序的请求，这些应用程序是为与AIR版本1.5及更早版本的客户端及受保护内容一起使用而创建的。

## 参考实施 {#reference-implementation}

该SDK包含一个参考实施，以及一个演示如何使用Java API的简单Adobe Primetime DRM部署。 参考实施提供了许可证服务器、Watched Folder Packager、Primetime DRM Manager AIR应用程序，以及用于基于Java API的内容打包和策略管理的命令行工具。 要了解有关Primetime DRM参考实施的更多信息，请参阅保护内容。
