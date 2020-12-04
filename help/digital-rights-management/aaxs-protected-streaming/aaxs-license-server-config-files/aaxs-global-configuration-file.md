---
seo-title: 全局配置文件
title: 全局配置文件
uuid: 10370bc0-36ab-4e43-9e75-c46a7177874c
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# 全局配置文件{#global-configuration-file}

flashaccess-global.xml配置文件包含适用于许可证服务器的所有租户的设置。 此文件必须位于&#x200B;*LicenseServer.ConfigRoot*&#x200B;中。 有关示例全局配置文件，请参阅configs目录。 全局配置文件包括：

* 缓存——控制内存中配置文件的缓存。 有关缓存设置的说明，请参阅“更新配置文件”。
* 日志记录——指定日志记录级别和滚动日志文件的频率。
* HSM密码——仅当使用HSM存储服务器凭据时才需要。

有关更多详细信息，请参阅位于`<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs`的示例全局配置文件中的注释。
