---
description: Primetime DRM的主要组件由Java SDK以及Flash Player和Adobe AIR客户端运行时环境组成。
seo-description: Primetime DRM的主要组件由Java SDK以及Flash Player和Adobe AIR客户端运行时环境组成。
seo-title: Java SDK、Flash Player和Adobe AIR客户端
title: Java SDK、Flash Player和Adobe AIR客户端
uuid: e6daed27-3803-4ef7-ba25-4a180af7502f
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Adobe Primetime DRM SDK {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM作为Java SDK提供，它提供可从中创建服务器实现的构件块。 使用SDK，您可以创建适合贵组织业务模式的Primetime DRM解决方案。

SDK中提供的Java API在以下子部分中有介绍。

## 用于管理设备组域的Java API{#java-apis-for-managing-device-group-domains}

这些API用于允许服务器处理加入和离开设备组域的客户端请求。

设备组域是能够彼此共享许可证的设备的逻辑集合。 要实现这一点，每台设备必须先加入／注册到同一域。 在服务器上运行的Primetime DRM SDK必须处理设备域加入（注册）请求以及设备域离开（注销）请求。 未加入任何域的设备将获得绑定到该设备的许可证，该许可证无法共享到任何其他设备。

## 用于保护内容的Java API{#java-apis-for-protecting-content}

这些API用于定义权限并准备要分发的内容。 内容保护API包括：

* 策略管理

   策略管理API用于创建和修改要应用于内容的策略。 可以创建或更新策略，包括获取／设置所有使用规则以及允许自定义命名空间中的其他参数。

* 内容打包

   内容打包API用于加密内容并从打包内容中检索元数据。

## 用于颁发许可证的Java API{#java-apis-for-issuing-licenses}

当客户端从服务器请求许可证时，会使用这些API。 SDK支持来自客户端的以下请求：

* 身份验证

   身份验证API可用于处理身份验证请求和生成身份验证令牌。

* 许可证生成和获取

   许可证生成和获取API用于为用户生成许可证。

* 支持Adobe AIR版本1.5客户端和内容

   为了向后兼容，SDK有API来处理来自AIR应用程序的请求，这些应用程序创建为与AIR版本1.5及更早版本的客户端及受保护的内容一起使用。

## 参考实现 {#reference-implementation}

SDK包括一个参考实施，一个简单的Adobe Primetime DRM部署，它演示了如何使用Java API。 该参考实施提供了用于基于Java API的内容打包和策略管理的许可证服务器、监视文件夹打包程序、Primetime DRM Manager AIR应用程序和命令行工具。 要进一步了解Primetime DRM参考实施，请参阅保护内容。