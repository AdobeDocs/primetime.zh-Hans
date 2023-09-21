---
title: 升级Adobe Primetime DRM服务器以进行受保护的流
description: 升级Adobe Primetime DRM服务器以进行受保护的流
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 升级Adobe Primetime DRM服务器以进行受保护的流{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

如果要升级运行Primetime DRM Server for Protected Streaming的服务器，您需要替换 `flashaccessserver.war` 使用最新Primetime DRM随附的文件部署到应用程序服务器上的文件。

如果要使用新的配置选项，则需要更新服务器的 `flashaccess-tenant.xml`. 您还需要更新 [!DNL jsafe.dll] 或 [!DNL libjsafe.so] 与最新的Primetime DRM随附的版本一起使用。
