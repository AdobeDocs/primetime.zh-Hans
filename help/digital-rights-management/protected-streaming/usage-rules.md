---
description: 使用Adobe PrimetimeDRM Server for Protected Streaming，您可以使用配置文件指定服务器上的所有使用规则。
seo-description: 使用Adobe PrimetimeDRM Server for Protected Streaming，您可以使用配置文件指定服务器上的所有使用规则。
seo-title: 关于使用规则
title: 关于使用规则
uuid: 4a794712-db58-43f5-b867-8871e58e12ae
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# 关于使用规则{#about-usage-rules}

使用Adobe PrimetimeDRM Server for Protected Streaming，您可以使用配置文件指定服务器上的所有使用规则。

在DRM策略中为受保护内容指定的任何使用规则都将被覆盖。 因此，Adobe建议您在内容打包过程中使用简单的匿名DRM策略。 您可以配置的任何使用规则都可以按租户进行配置。

Primetime DRM Server for Protected Streaming支持以下使用规则：

* 输出保护
* Adobe® AIR®、SWF、iOS和Android应用程序限制
* DRM和运行时模块限制
* 在支持越狱检测的Primetime DRM平台上的越狱检测实施
* 默认情况下，许可证缓存处于禁用状态。 可通过指定缓存结束日期或允许缓存时间量启用的许可证缓存；开始许可证的颁发时间。
* 多个播放权限，允许您指定输出保护、应用程序限制和DRM/运行时限制的不同组合。 例如，您可以使用DRM模块限制和输出保护为每个客户端平台指定不同的输出保护要求。

>[!NOTE]
>
>如果要支持对iOS设备的远程密钥投放，则在打包时应用的DRM策略必须启用远程密钥投放。 无法通过服务器上的租户配置修改此设置。

