---
seo-title: 标准AAXS DRM工作流程
title: 标准AAXS DRM工作流程
description: 标准AAXS DRM工作流程
seo-description: 标准AAXS DRM工作流程
uuid: b996eb2c-8e37-4a29-a972-e09c69d2461d
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 标准AAXS DRM工作流{#standard-aaxs-drm-workflow}

1. （包）AAXS Java SDK生成随机CEK。
1. （包）CEK用于加密内容。
1. （包）CEK使用AAXS许可证服务器的公钥进行加密。
1. （包）加密的CEK会插入内容的DRM元数据中。
1. 设备尝试通过从AAXS服务器请求许可证来播放内容。
1. （授权）AAXS服务器使用其私钥从元数据解密CEK。
1. （许可）AAXS服务器向设备颁发包含CEK的许可证。
