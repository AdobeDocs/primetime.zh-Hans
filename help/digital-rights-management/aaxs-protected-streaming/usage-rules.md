---
seo-title: 使用规则
title: 使用规则
uuid: 361d07b9-e4c8-47ab-8c45-a1de98c9fed7
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 使用规则{#usage-rules}

使用Adobe Access Server的受保护流，通过配置文件在服务器上指定所有使用规则。 受保护内容中指定的任何使用规则都会被覆盖，因此建议在内容打包过程中使用简单的匿名策略。 可以按租户设置可配置的使用规则。

Adobe Access Server的受保护流支持以下使用规则：

* 输出保护
* Adobe® AIR®、SWF、iOS和Android应用程序限制
* DRM和运行时模块限制
* 越狱检测强制(在支持越狱检测的Adobe访问平台上)
* 默认情况下，许可证缓存处于禁用状态。 可以通过指定缓存结束日期或允许时间缓存（从颁发许可证开始）来启用许可证缓存。
* 多播放权限，通过它可指定输出保护、应用程序限制和DRM/运行时限制的不同组合。 例如，可以通过使用带输出保护的DRM模块限制为每个客户端平台指定不同的输出保护要求。

>[!NOTE]
>
>要支持对iOS设备的远程密钥投放，在打包时使用的策略必须启用远程密钥投放。 无法通过服务器上的租户配置修改此设置。 ***Adobe Primetime需要构建能够播放受Adobe访问保护的内容的iOS应用程序。***

