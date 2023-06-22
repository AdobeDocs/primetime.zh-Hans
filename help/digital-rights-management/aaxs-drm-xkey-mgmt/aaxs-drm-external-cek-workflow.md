---
title: AAXS DRM外部CEK工作流
description: 此工作流与大多数现有DRM系统不同，因为它不需要使用任何中央存储库或内容密钥管理系统(CKMS)
exl-id: f084aa57-8bef-40a0-b52d-4d23dfdf36c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# AAXS DRM外部CEK工作流{#aaxs-drm-external-cek-workflow}

此工作流与大多数现有DRM系统不同，因为它不需要使用任何中央存储库或内容密钥管理系统(CKMS)。 但是，对于希望AAXS与其现有CKMS结合使用的客户，AAXS提供了一个称为“外部CEK”的功能，其中CEK在打包和许可证颁发时从外部提供。

![](assets/ECEK_Workflow.PNG)

1. （包）为AAXS Java SDK提供CEK和CEK ID。
1. （包） CEK用于加密内容。
1. （包）CEK ID会插入到内容的DRM元数据中。
1. 该设备尝试通过向AAXS服务器请求许可证来播放内容。
1. （许可） AAXS服务器从内容元数据中提取CEK ID。
1. AAXS服务器从CKMS检索CEK。
1. （许可） AAXS服务器向设备颁发包含CEK的许可证。
