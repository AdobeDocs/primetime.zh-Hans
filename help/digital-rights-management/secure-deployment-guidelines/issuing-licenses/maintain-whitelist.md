---
description: 允许列表是可信实体的列表。
title: 维护可信内容打包者的允许列表
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 维护受信任内容包装程序的允许列表{#maintain-a-allowlist-of-trusted-content-packagers}

允许列表是可信实体的列表。

对于内容打包者，实体是内容所有者信任的组织，可以打包（或加密）视频文件并创建DRM保护的内容。 部署Adobe Primetime DRM时，应保持受信任内容包装程序的允许列表。 在颁发许可证之前，还必须验证受DRM保护的文件的DRM元数据中内容打包程序的身份。

要了解如何获取有关打包内容的实体的信息，请参阅[V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())。
