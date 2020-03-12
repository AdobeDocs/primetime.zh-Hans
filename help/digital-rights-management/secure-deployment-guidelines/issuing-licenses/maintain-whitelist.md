---
description: 白名单是受信任实体的列表。
seo-description: 白名单是受信任实体的列表。
seo-title: 维护受信任的内容包装程序的白名单
title: 维护受信任的内容包装程序的白名单
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 维护受信任的内容包装程序的白名单{#maintain-a-whitelist-of-trusted-content-packagers}

白名单是受信任实体的列表。

对于内容打包程序，实体是内容所有者信任的组织，可以打包（或加密）视频文件并创建DRM保护的内容。 部署Adobe Primetime DRM时，您应当保留受信任内容打包程序的白名单。 在发布许可证之前，还必须验证受DRM保护的文件的DRM元数据中的内容打包程序的标识。

要了解如何获取有关打包内容的实体的信息，请参 [阅V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())。
