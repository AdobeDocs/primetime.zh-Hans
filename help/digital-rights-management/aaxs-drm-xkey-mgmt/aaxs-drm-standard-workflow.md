---
title: 标准AAXS DRM工作流
description: 标准AAXS DRM工作流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 标准AAXS DRM工作流{#standard-aaxs-drm-workflow}

1. （包）AAXS Java SDK生成随机CEK。
1. （包）CEK用于加密内容。
1. （包）CEK使用AAXS License Server的公钥加密。
1. （包）加密的CEK将插入内容的DRM元数据中。
1. 设备尝试通过从AAXS服务器请求许可证来播放内容。
1. （许可）AAXS服务器使用其私钥从元数据解密CEK。
1. （许可）AAXS服务器向设备颁发包含CEK的许可证。
