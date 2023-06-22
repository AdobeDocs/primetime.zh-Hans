---
description: 客户可以将Adobe访问(AAXS) DRM与其自己的内容密钥管理系统(CKMS)结合使用以及外部CEK功能。
title: Adobe访问DRM外部CEK概述
exl-id: 4131863b-5773-4222-aae9-d984267cdb86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Adobe访问DRM外部CEK概述 {#adobe-access-drm-external-cek-overview}

客户可以将Adobe访问(AAXS) DRM与其自己的内容密钥管理系统(CKMS)结合使用以及外部CEK功能。

默认情况下，Adobe访问(AAXS) DRM抽象出在内容打包过程中直接处理密钥、证书和DRM元数据的需要。 AAXS Java SDK将在打包期间自动生成随机内容加密密钥(CEK)，并使用它来加密内容。 接下来，SDK会加密CEK本身，并将其插入到内容的元数据中。 在许可证颁发时，AAXS服务器只需要其AAXS许可证服务器私钥即可从元数据访问CEK来生成许可证。
