---
title: 维护受信任内容打包程序的允许列表
description: 维护受信任内容打包程序的允许列表
copied-description: true
exl-id: 4c296d23-75c1-4d0b-a636-31b49e99c753
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# 维护受信任内容打包程序的允许列表 {#maintain-a-allowlist-of-trusted-content-packagers}

An **允许列表** 是受信任实体的列表。 对于内容打包程序，它们是受内容所有者信任的组织，用于打包（或加密）FLV/F4V视频文件，从而创建受DRM保护的内容。 在部署Adobe访问时，建议您维护一个受信任的内容打包程序的允许列表，并在颁发许可证之前验证受DRM保护文件的DRM元数据（DRM标头）中包含的内容打包程序的身份。

要了解有关获取有关打包内容的实体的信息的更多信息，请参阅 `V2ContentMetaData.getPackagerInfo()` 在 *Adobe访问API参考*.
