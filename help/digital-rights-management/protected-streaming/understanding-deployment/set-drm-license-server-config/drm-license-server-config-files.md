---
title: 许可证服务器配置文件
description: 许可证服务器配置文件
copied-description: true
exl-id: d48e88a4-caae-4f4e-b870-38da4f3a715e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# 许可证服务器配置文件{#license-server-configuration-files}

Adobe Primetime DRM Server for Protected Streaming需要以下类型的配置文件：

* 全局配置文件( [!DNL flashaccess-global.xml])
* 每个租户( [!DNL flashaccess-tenant.xml])

完成配置文件编辑后，Adobe建议您使用Primetime DRM Server for Protected Streaming随附的实用程序来验证文件的格式是否正确。

参见 *配置验证器*.

如果要避免在配置文件中以明文形式提供口令，则必须使用Adobe提供的Scrambler工具加密在全局和租户配置文件中指定的所有口令。

参见 *密码加扰器* 有关如何加密密码的详细信息。
