---
title: 全局配置文件
description: 全局配置文件
copied-description: true
exl-id: 5a2f96fe-d39d-4391-a010-200a900b043b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 全局配置文件{#global-configuration-file}

flashaccess-global.xml配置文件包含适用于许可证服务器所有租户的设置。 此文件必须位于 *LicenseServer.ConfigRoot*. 有关示例全局配置文件，请参阅configs目录。 全局配置文件包含以下内容：

* 高速缓存 — 控制内存中配置文件的高速缓存。 有关缓存设置的说明，请参阅更新配置文件。
* 事件记录 — 指定事件记录级别和日志文件的滚动频率。
* HSM密码 — 仅当使用HSM存储服务器凭据时才需要。

请参见位于以下位置的示例全局配置文件中的注释： `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` 了解更多详细信息。
