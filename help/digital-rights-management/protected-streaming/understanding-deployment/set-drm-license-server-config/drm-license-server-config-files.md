---
title: 许可证服务器配置文件
description: 许可证服务器配置文件
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 许可证服务器配置文件{#license-server-configuration-files}

Adobe Primetime DRM Server for Protected Streaming需要以下类型的配置文件：

* 全局配置文件([!DNL flashaccess-global.xml])
* 每个租户的租户配置文件([!DNL flashaccess-tenant.xml])

在您完成配置文件编辑后，Adobe建议您使用随Primetime DRM Server for Protected Streaming提供的实用程序来验证文件的格式是否正确。

请参阅&#x200B;*Configuration Validator*。

如果您希望避免在配置文件中以明文形式提供口令，则必须使用Adobe提供的Scrambler工具加密在全局配置文件和租户配置文件中指定的所有口令。

有关如何加密密码的详细信息，请参阅&#x200B;*密码剪贴器*。
