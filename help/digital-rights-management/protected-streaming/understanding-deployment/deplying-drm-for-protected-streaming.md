---
title: 部署Adobe Primetime DRM Server以实现受保护的流
description: 部署Adobe Primetime DRM Server以实现受保护的流
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 部署受保护流{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}的Adobe Primetime DRM服务器

在部署Adobe Primetime DRM Server以用于受保护流之前，必须已安装Java和Tomcat版本，如“要求”主题中所列。

用于受保护流的Primetime DRM服务器包包括[!DNL flashaccesserver.war]。 如果您：

* 要部署此WAR文件，需要将其复制到Tomcat的[!DNL webapps]目录。
* 以前已部署WAR文件，您可能需要删除解压缩的WAR目录（Tomcat的[!DNL webapps]目录中的[!DNL flashaccessserver]）。

* 要阻止Tomcat解包WAR文件，请编辑Tomcat的[!DNL conf]目录中的[!DNL server.xml]文件，并通过将`unpackWARs`属性设置为`false`来配置属性。

>[!NOTE]
>
>如果已将Tomcat配置为在系统类路径中包含[!DNL commons-logging.jar]（Primetime DRM Server for Protected Streaming不是必需的），则必须配置commons-logging才能使用Log4J。

服务器可以选择使用平台特定的库(Microsoft Windows上的[!DNL jsafe.dll]或Linux上的[!DNL libjsafe.so]以获得最佳性能。 您可以将平台的相应库从&#x200B;[!DNL thirdparty/cryptoj/]*platform*&#x200B;复制到由Linux上的`PATH`环境变量或`LD_LIBRARY_PATH`指定的位置。

>[!NOTE]
>
>仅当操作系统和JDK都支持64位时，才应使用64位版本。 否则，您需要使用32位版本。

