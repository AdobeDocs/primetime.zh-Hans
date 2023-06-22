---
title: 使用规则
description: 使用规则
copied-description: true
exl-id: 0f6df09f-47fd-4a05-bcb0-786beaba325a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 使用规则{#usage-rules}

使用Adobe Access Server for Protected Streaming，所有使用规则都通过配置文件在服务器上指定。 受保护内容中指定的任何使用规则都会被覆盖，因此建议在内容打包期间使用简单的匿名策略。 可配置的使用规则可以根据租户进行设置。

适用于受保护流的Adobe Access Server支持以下使用规则：

* 输出保护
* Adobe® AIR®、SWF、iOS和Android应用程序限制
* DRM和运行时模块限制
* 越狱检测实施(在支持越狱检测的Adobe访问平台上)
* 默认情况下，许可证缓存处于禁用状态。 可以通过指定缓存结束日期或允许缓存的时间量（从颁发许可证时开始）来启用许可证缓存。
* 多个播放权限，可让您指定输出保护、应用程序限制和DRM/运行时限制的不同组合。 例如，可以使用带有输出保护的DRM模块限制为每个客户端平台指定不同的输出保护要求。

>[!NOTE]
>
>要支持将远程密钥交付到iOS设备，打包时使用的策略必须启用远程密钥交付。 无法通过服务器上的租户配置修改此设置。 ***需要Adobe Primetime才能构建可播放受Adobe访问保护内容的iOS应用程序。***
