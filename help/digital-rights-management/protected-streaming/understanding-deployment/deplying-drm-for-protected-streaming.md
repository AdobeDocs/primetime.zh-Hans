---
title: 为受保护的流部署Adobe Primetime DRM Server
description: 为受保护的流部署Adobe Primetime DRM Server
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 为受保护的流部署Adobe Primetime DRM Server{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

在部署Adobe Primetime DRM Server for Protected Streaming之前，必须已安装“要求”主题中列出的Java和Tomcat版本。

Primetime DRM Server for Protected Streaming包包括 [!DNL flashaccesserver.war]. 如果您：

* 要部署此WAR文件，您需要将其复制到Tomcat的 [!DNL webapps] 目录。
* 以前部署过WAR文件，您可能需要删除解压缩的WAR目录( [!DNL flashaccessserver] 在Tomcat的 [!DNL webapps] 目录)。

* 要阻止Tomcat解压缩WAR文件，请编辑 [!DNL server.xml] tomcat中的文件 [!DNL conf] 目录并配置 `unpackWARs` 属性，方法是将其设置为 `false`.

>[!NOTE]
>
>如果已将Tomcat配置为包含 [!DNL commons-logging.jar] 在系统类路径上（Primetime DRM Server for Protected Streaming不需要），必须配置commons-logging以使用Log4J。

服务器可以选择使用特定于平台的库( [!DNL jsafe.dll] 在Microsoft Windows上或 [!DNL libjsafe.so] 在Linux上以获得最佳性能。 您可以从以下位置复制适用于您的平台的库： [!DNL thirdparty/cryptoj/]*平台* 到由指定的位置 `PATH` 环境变量或 `LD_LIBRARY_PATH` 在Linux上。

>[!NOTE]
>
>仅当操作系统和JDK都支持64位时，才应使用64位版本。 否则，您需要使用32位版本。
