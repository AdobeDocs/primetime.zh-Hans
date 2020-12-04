---
description: 允许列表是受信任实体的列表。
seo-description: 允许列表是受信任实体的列表。
seo-title: 维护可信内容包装程序的允许列表
title: 维护可信内容包装程序的允许列表
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# 维护受信任内容包装程序的允许列表{#maintain-a-allowlist-of-trusted-content-packagers}

允许列表是受信任实体的列表。

对于内容打包者，实体是内容所有者信任的组织，可以打包（或加密）视频文件并创建DRM保护的内容。 部署Adobe PrimetimeDRM时，您应当维护一允许列表可信的内容打包程序。 在颁发许可证之前，还必须验证受DRM保护的文件的DRM元数据中的内容打包程序的身份。

要了解如何获取有关打包内容的实体的信息，请参阅[V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())。
