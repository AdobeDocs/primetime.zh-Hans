---
title: Primetime Cloud DRM不支持的内容
description: Primetime Cloud DRM不支持的内容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Primetime Cloud DRM不支持的内容{#what-is-not-supported-by-primetime-cloud-drm}

Primetime Cloud DRM支持当前在Primetime DRM中可用的几乎所有功能。 但是，由于某些DRM功能需要与客户的后端业务规则子系统通信，因此某些功能在Primetime Cloud DRM中不可用。

Primetime Cloud DRM当前不支持的功能包括：

* 与外部CEK打包的内容（其中，许可证服务器从外部密钥管理系统请求内容的CEK）
* 设备域
* 高级许可证链接
* 许可证退回/撤销
* PHLS/PHDS。 这些保护方案不使用许可证服务器
* 用户/密码身份验证
