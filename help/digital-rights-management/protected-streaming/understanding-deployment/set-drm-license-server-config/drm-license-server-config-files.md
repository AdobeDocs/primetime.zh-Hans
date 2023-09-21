---
title: 许可证服务器配置文件
description: 许可证服务器配置文件
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 许可证服务器配置文件{#license-server-configuration-files}

Adobe Primetime DRM Server for Protected Streaming需要以下类型的配置文件：

* 全局配置文件( [!DNL flashaccess-global.xml])
* 每个租户的租户配置文件( [!DNL flashaccess-tenant.xml])

完成配置文件编辑后，Adobe建议您使用Primetime DRM Server for Protected Streaming随附的实用程序来验证文件的格式是否正确。

请参阅 *配置验证器*.

如果您希望避免在配置文件中以明文形式提供密码，则必须使用Adobe提供的Scrambler工具对您在全局配置文件和租户配置文件中指定的所有密码进行加密。

请参阅 *密码加扰器* 有关如何加密密码的详细信息。
