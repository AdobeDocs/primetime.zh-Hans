---
seo-title: 升级Adobe Primetime DRM Server，实现受保护的流
title: 升级Adobe Primetime DRM Server，实现受保护的流
uuid: 5c507ae3-d1d9-40ad-ba97-501ec92b45dc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 升级Adobe Primetime DRM Server，实现受保护的流{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

如果要升级运行Primetime DRM Server以实现受保护流的服务器，您需要将应用程序服务器上部署的文件替换为最新Primetime DRM包含的文件。 `flashaccessserver.war`

如果要使用新的配置选项，则需要更新服务器的配置选项 `flashaccess-tenant.xml`。 您还需要更新 [!DNL jsafe.dll] 或 [!DNL libjsafe.so] 更新最新Primetime DRM附带的版本。
