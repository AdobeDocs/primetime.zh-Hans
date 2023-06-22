---
title: 升级Adobe Primetime DRM服务器以进行受保护的流
description: 升级Adobe Primetime DRM服务器以进行受保护的流
copied-description: true
exl-id: 6edfba1b-46a2-4cbd-bc14-feeef1a36ed6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 升级Adobe Primetime DRM服务器以进行受保护的流{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

如果要升级运行Primetime DRM Server for Protected Streaming的服务器，您需要替换 `flashaccessserver.war` 使用随最新Primetime DRM一起提供的文件部署在应用程序服务器上的文件。

如果要使用新的配置选项，则需要更新服务器的 `flashaccess-tenant.xml`. 您还需要更新 [!DNL jsafe.dll] 或 [!DNL libjsafe.so] 与最新的Primetime DRM随附的版本一起使用。
