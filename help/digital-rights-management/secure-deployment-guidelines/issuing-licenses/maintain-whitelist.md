---
description: 允许列表是受信任实体的列表。
title: 维护受信任内容打包程序的允许列表
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 维护受信任内容打包程序的允许列表 {#maintain-a-allowlist-of-trusted-content-packagers}

允许列表是受信任实体的列表。

对于内容打包员，实体是内容所有者信任的组织，用于打包（或加密）视频文件并创建受DRM保护的内容。 在部署Adobe Primetime DRM时，您应该维护一个受信任的内容打包程序的允许列表。 在颁发许可证之前，您还必须验证受DRM保护文件的DRM元数据中的内容打包器的身份。

要了解如何获取有关打包内容的实体的信息，请参阅 [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
