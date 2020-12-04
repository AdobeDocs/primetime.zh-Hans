---
seo-title: 升级Adobe PrimetimeDRM服务器以实现受保护的流
title: 升级Adobe PrimetimeDRM服务器以实现受保护的流
uuid: 5c507ae3-d1d9-40ad-ba97-501ec92b45dc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 升级Adobe PrimetimeDRM服务器以实现受保护的流{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

如果要升级运行受保护流的Primetime DRM服务器的服务器，您需要用最新Primetime DRM中包含的文件替换在应用程序服务器上部署的`flashaccessserver.war`文件。

如果要使用新的配置选项，则需要更新服务器的`flashaccess-tenant.xml`。 您还需要使用最新Primetime DRM附带的版本更新[!DNL jsafe.dll]或[!DNL libjsafe.so]。
