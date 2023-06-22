---
title: 标准AAXS DRM工作流
description: 标准AAXS DRM工作流
exl-id: 3bc6aa6a-cda6-4c83-af08-f27eb103a47a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 标准AAXS DRM工作流{#standard-aaxs-drm-workflow}

1. （包） AAXS Java SDK生成一个随机CEK。
1. （包） CEK用于加密内容。
1. （包） CEK使用AAXS License Server的公共密钥进行加密。
1. （包）加密的CEK插入到内容的DRM元数据中。
1. 该设备尝试通过向AAXS服务器请求许可证来播放内容。
1. （许可） AAXS服务器使用其私钥从元数据中解密CEK。
1. （许可） AAXS服务器向设备颁发包含CEK的许可证。
