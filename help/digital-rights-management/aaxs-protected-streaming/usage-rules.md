---
seo-title: 使用规则
title: 使用规则
uuid: 361d07b9-e4c8-47ab-8c45-a1de98c9fed7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用规则{#usage-rules}

使用Adobe Access Server for Protected Streaming，所有使用规则都通过配置文件在服务器上指定。 受保护内容中指定的任何使用规则都会被覆盖，因此建议在内容打包过程中使用简单的匿名策略。 可以按租户设置可配置的使用规则。

Adobe Access Server for Protected Streaming支持以下使用规则：

* 输出保护
* Adobe® AIR®、SWF、iOS和Android应用程序限制
* DRM和运行时模块限制
* 越狱检测强制（在支持越狱检测的Adobe Access平台上）
* 默认情况下，许可证缓存处于禁用状态。 可以通过指定缓存结束日期或允许的缓存时间量（从发布许可证开始）来启用许可证缓存。
* 多播放权限，它允许您指定输出保护、应用程序限制和DRM/运行时限制的不同组合。 例如，可以通过使用DRM模块限制和输出保护为每个客户端平台指定不同的输出保护要求。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>要支持向iOS设备远程交付密钥，打包时使用的策略必须启用远程密钥交付。 无法通过服务器上的租户配置修改此设置。 ***需要Adobe Primetime构建可播放Adobe Access保护内容的iOS应用程序。***

