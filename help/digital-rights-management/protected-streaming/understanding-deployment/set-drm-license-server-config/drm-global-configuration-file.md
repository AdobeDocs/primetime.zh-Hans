---
description: flashaccess-global.xml配置文件包括适用于许可证服务器的所有租户的设置。
seo-description: flashaccess-global.xml配置文件包括适用于许可证服务器的所有租户的设置。
seo-title: 全局配置文件
title: 全局配置文件
uuid: 294d6cff-be07-4b4b-8aa6-943044a1c56f
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# 全局配置文件{#global-configuration-file}

flashaccess-global.xml配置文件包括适用于许可证服务器的所有租户的设置。

必须将配置文件放在[!DNL LicenseServer.ConfigRoot]目录中。

有关全局配置文件的示例，请参见[!DNL configs]目录。

全局配置文件包括：

* 缓存——控制内存中配置文件的缓存。

   有关缓存设置的信息，请参阅&#x200B;*更新配置文件*。
* 日志记录——指定日志记录级别和滚动日志文件的频率。
* HSM密码——仅当使用HSM存储服务器凭据时才需要。

有关更多详细信息，请参阅Primetime DRM `<DVD>`\Adobe PrimetimeDRM Server for Protected Streaming\configs中的示例全局配置文件中的注释。
