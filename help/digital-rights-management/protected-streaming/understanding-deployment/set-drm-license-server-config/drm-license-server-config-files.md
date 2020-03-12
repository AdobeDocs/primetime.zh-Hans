---
seo-title: 许可证服务器配置文件
title: 许可证服务器配置文件
uuid: 7c7e0f76-2ced-45af-9542-99e06ec31cda
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 许可证服务器配置文件{#license-server-configuration-files}

Adobe Primetime DRM Server for Protected Streaming需要以下类型的配置文件：

* 全局配置文件( [!DNL flashaccess-global.xml])
* 每个租户的租户配置文件( [!DNL flashaccess-tenant.xml])

在您完成配置文件编辑后，Adobe建议您使用随Primetime DRM Server提供的用于受保护流的实用程序来验证文件的格式是否正确。

请参 *阅配置验证程序*。

如果要避免在配置文件中以明文形式提供口令，则必须使用Adobe提供的Scrambler工具加密在全局和租户配置文件中指定的所有口令。

有关如 *何加密密码的更多信息* ，请参阅密码剪贴器。
