---
title: 升级Adobe Primetime DRM服务器以实现受保护的流
description: 升级Adobe Primetime DRM服务器以实现受保护的流
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 升级Adobe Primetime DRM Server for Protected Streaming{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

如果要升级运行受保护流的Primetime DRM服务器的服务器，您需要用最新Primetime DRM包含的文件替换已部署在应用程序服务器上的`flashaccessserver.war`文件。

如果要使用新的配置选项，则需要更新服务器的`flashaccess-tenant.xml`。 您还需要使用最新Primetime DRM附带的版本更新[!DNL jsafe.dll]或[!DNL libjsafe.so]。
