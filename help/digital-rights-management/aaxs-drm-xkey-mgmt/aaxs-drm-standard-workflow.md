---
title: 标准AAXS DRM工作流
description: 标准AAXS DRM工作流
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 标准AAXS DRM工作流{#standard-aaxs-drm-workflow}

1. （包） AAXS Java SDK生成一个随机CEK。
1. （包）CEK用于加密内容。
1. （包）使用AAXS许可证服务器的公钥加密CEK。
1. （包）加密的CEK插入到内容的DRM元数据中。
1. 该设备通过向AAXS服务器请求许可证来尝试播放内容。
1. （许可） AAXS服务器使用其私钥从元数据中解密CEK。
1. （许可） AAXS服务器向设备颁发包含CEK的许可证。
