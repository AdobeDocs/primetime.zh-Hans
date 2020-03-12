---
description: 客户可以将Adobe Access(AAXS)DRM与其自己的内容密钥管理系统(CKMS)结合使用外部CEK功能。
seo-description: 客户可以将Adobe Access(AAXS)DRM与其自己的内容密钥管理系统(CKMS)结合使用外部CEK功能。
seo-title: Adobe Access DRM External CEK概述
title: Adobe Access DRM External CEK概述
uuid: ea0bba63-7743-4216-863f-392500998eb6
translation-type: tm+mt
source-git-commit: 92e04cbb5e94f60c8d06e94b826ff9361c10ef97

---


# Adobe Access DRM External CEK概述 {#adobe-access-drm-external-cek-overview}

客户可以将Adobe Access(AAXS)DRM与其自己的内容密钥管理系统(CKMS)结合使用外部CEK功能。

默认情况下，Adobe Access(AAXS)DRM提取了在内容打包过程中直接处理密钥、证书和DRM元数据的需求。 AAXS Java SDK将在打包期间自动生成随机内容加密密钥(CEK)，并使用它加密内容。 接下来，SDK加密CEK本身，并将其插入内容的元数据中。 在许可证发放时，AAXS服务器只需要其AAXS许可证服务器私钥即可从元数据访问CEK以生成许可证。
