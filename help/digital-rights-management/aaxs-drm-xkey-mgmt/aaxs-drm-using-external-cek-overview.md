---
description: 客户可以将Adobe Access(AAXS)DRM与其自己的内容密钥管理系统(CKMS)结合外部CEK功能使用。
title: Adobe访问DRM外部CEK概述
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Adobe访问DRM外部CEK概述{#adobe-access-drm-external-cek-overview}

客户可以将Adobe Access(AAXS)DRM与其自己的内容密钥管理系统(CKMS)结合外部CEK功能使用。

Adobe访问(AAXS)DRM默认在内容打包过程中提取直接处理密钥、证书和DRM元数据的需求。 AAXS Java SDK将在打包时自动生成随机内容加密密钥(CEK)，并使用它加密内容。 接下来，SDK加密CEK本身，并将其插入内容的元数据中。 在许可证颁发时，AAXS服务器只需要其AAXS许可证服务器私钥即可从元数据访问CEK以生成许可证。
