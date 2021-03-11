---
title: 维护可信内容打包者的允许列表
description: 维护可信内容打包者的允许列表
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 维护受信任内容包装程序的允许列表{#maintain-a-allowlist-of-trusted-content-packagers}

**允许列表**&#x200B;是可信实体的列表。 对于内容打包者，这些是内容所有者信任的组织来打包（或加密）FLV/F4V视频文件，从而创建DRM保护的内容。 部署Adobe访问时，建议您保持受信任内容包装程序的允许列表，并在发放许可证之前验证DRM保护文件的DRM元数据（DRM头）中包含的内容包装程序的标识。

要了解有关获取有关打包内容的实体的信息，请参阅&#x200B;*Adobe访问API参考*&#x200B;中的`V2ContentMetaData.getPackagerInfo()`。
