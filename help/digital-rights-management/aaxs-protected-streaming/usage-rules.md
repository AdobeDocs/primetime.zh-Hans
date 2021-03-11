---
title: 使用规则
description: 使用规则
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 使用规则{#usage-rules}

使用Adobe Access Server for Protected Streaming，通过配置文件在服务器上指定所有使用规则。 在受保护内容中指定的任何使用规则都将被覆盖，因此建议在内容打包过程中使用简单的匿名策略。 可以按租户设置可配置的使用规则。

Adobe Access Server for Protected Streaming支持以下使用规则：

* 输出保护
* Adobe® AIR®、SWF、iOS和Android应用程序限制
* DRM和运行时模块限制
* 越狱检测强制(在支持越狱检测的Adobe访问平台上)
* 默认情况下，许可证缓存处于禁用状态。 可以通过指定缓存结束日期或允许的时间缓存（从颁发许可证开始）来启用许可证缓存。
* 多播放权限，可让您指定不同的输出保护、应用程序限制和DRM/运行时限制组合。 例如，可以通过使用带输出保护的DRM模块限制为每个客户端平台指定不同的输出保护要求。

>[!NOTE]
>
>要支持对iOS设备的远程密钥投放，打包时使用的策略必须启用远程密钥投放。 无法通过服务器上的租户配置修改此设置。 ***Adobe Primetime是构建可以播放受Adobe Access保护的内容的iOS应用程序所必需的。***

