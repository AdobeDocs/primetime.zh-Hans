---
seo-title: AAXS DRM外部CEK工作流
title: AAXS DRM外部CEK工作流
description: 此工作流程与大多数现有DRM系统不同，因为它不需要使用任何中央存储库或内容密钥管理系统(CKMS)
seo-description: 此工作流程与大多数现有DRM系统不同，因为它不需要使用任何中央存储库或内容密钥管理系统(CKMS)
uuid: b313594b-0feb-4f27-bf02-f04b955e2140
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc

---


# AAXS DRM外部CEK工作流{#aaxs-drm-external-cek-workflow}

此工作流程与大多数现有DRM系统不同，因为它不需要使用任何中央存储库或内容密钥管理系统(CKMS)。 但是，对于希望AAXS与其现有CKMS合作的客户，AAXS提供一个名为“外部CEK”的功能，该功能中CEK在包装和许可发行时由外部提供。

![](assets/ECEK_Workflow.PNG)

1. （包）AAXS Java SDK提供有CEK和CEK ID。
1. （包）CEK用于加密内容。
1. （包）CEK ID将插入内容的DRM元数据中。
1. 设备尝试通过从AAXS服务器请求许可证来播放内容。
1. （许可）AAXS服务器从内容元数据中提取CEK ID。
1. AAXS服务器从CKMS中检索CEK。
1. （许可）AAXS服务器向设备发出包含CEK的许可。
