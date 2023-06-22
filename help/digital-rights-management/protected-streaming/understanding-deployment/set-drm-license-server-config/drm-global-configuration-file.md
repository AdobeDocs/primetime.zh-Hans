---
description: flashaccess-global.xml配置文件包含适用于许可证服务器所有租户的设置。
title: 全局配置文件
exl-id: 3e74bce6-1634-469f-9d02-1121e9d50687
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 全局配置文件{#global-configuration-file}

flashaccess-global.xml配置文件包含适用于许可证服务器所有租户的设置。

必须将配置文件放入 [!DNL LicenseServer.ConfigRoot] 目录。

请参阅 [!DNL configs] 目录作为全局配置文件的示例。

全局配置文件包括：

* 高速缓存 — 控制内存中配置文件的高速缓存。

   参见 *更新配置文件* 有关缓存设置的信息。
* 事件记录 — 指定事件记录级别和日志文件的滚动频率。
* HSM密码 — 仅当使用HSM存储服务器凭据时才需要。

请参阅位于Primetime DRM中的示例全局配置文件中的注释 `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs ，以了解更多详细信息。
