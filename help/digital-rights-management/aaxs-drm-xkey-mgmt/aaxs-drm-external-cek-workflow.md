---
title: AAXS DRM外部CEK工作流
description: 此工作流不同于大多数现有的DRM系统，因为它不需要使用任何中央存储库或内容密钥管理系统(CKMS)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# AAXS DRM外部CEK工作流{#aaxs-drm-external-cek-workflow}

此工作流不同于大多数现有的DRM系统，因为它不需要使用任何中央存储库或内容密钥管理系统(CKMS)。 但是，对于希望AAXS能够与其现有CKMS配合使用的客户，AAXS提供了“外部CEK”功能，在打包和颁发许可证时，CEK会从外部提供。

![](assets/ECEK_Workflow.PNG)

1. （包） AAXS Java SDK提供了CEK和CEK ID。
1. （包）CEK用于加密内容。
1. （包）CEK ID会插入到内容的DRM元数据中。
1. 该设备通过向AAXS服务器请求许可证来尝试播放内容。
1. （许可） AAXS服务器从内容元数据中提取CEK ID。
1. AAXS服务器从CKMS中检索CEK。
1. （许可） AAXS服务器向设备颁发包含CEK的许可证。
