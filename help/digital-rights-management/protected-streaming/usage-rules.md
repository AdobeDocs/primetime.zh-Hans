---
description: 使用Adobe Primetime DRM Server for Protected Streaming，您可以指定服务器上的所有使用规则，以及配置文件。
title: 关于使用规则
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# 关于使用规则{#about-usage-rules}

使用Adobe Primetime DRM Server for Protected Streaming，您可以指定服务器上的所有使用规则，以及配置文件。

在DRM策略中为受保护内容指定的任何使用规则都将被覆盖。 因此，Adobe建议您在内容打包期间使用简单的匿名DRM策略。 您可以配置的任何使用规则都可以基于每个租户进行配置。

Primetime DRM Server for Protected Streaming支持以下使用规则：

* 输出保护
* Adobe® AIR®、SWF、iOS和Android应用程序限制
* DRM和运行时模块限制
* 支持越狱检测的Primetime DRM平台上的越狱检测强制执行
* 默认情况下，许可证缓存处于禁用状态。 可以通过指定缓存结束日期或允许缓存的时间量来启用的许可证缓存；它会在颁发许可证时启动。
* 多个播放权限，可让您指定“输出保护”、“应用程序限制”和“DRM/运行时限制”的不同组合。 例如，可以使用带有输出保护的DRM模块限制为每个客户端平台指定不同的输出保护要求。

>[!NOTE]
>
>如果要支持将远程密钥交付到iOS设备，则打包时应用的DRM策略必须启用远程密钥交付。 无法通过服务器上的租户配置修改此设置。
