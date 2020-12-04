---
seo-title: 部署Adobe PrimetimeDRM服务器以实现受保护的流
title: 部署Adobe PrimetimeDRM服务器以实现受保护的流
uuid: 83ef8237-0026-4677-b42b-ea4b6de19630
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 部署Adobe PrimetimeDRM服务器以实现受保护的流{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

在部署Adobe PrimetimeDRM Server for Protected Streaming之前，必须已安装Java和Tomcat的版本，如“要求”主题中所列。

用于受保护流的Primetime DRM服务器包包括[!DNL flashaccesserver.war]。 如果您：

* 要部署此WAR文件，您需要将其复制到Tomcat的[!DNL webapps]目录。
* 以前已部署WAR文件，您可能需要删除未打包的WAR目录（Tomcat的[!DNL webapps]目录中的[!DNL flashaccessserver]）。

* 要阻止Tomcat解包WAR文件，请编辑Tomcat的[!DNL conf]目录中的[!DNL server.xml]文件，并通过将`unpackWARs`属性设置为`false`来配置该属性。

>[!NOTE]
>
>如果已将Tomcat配置为在系统类路径中包含[!DNL commons-logging.jar]（Primetime DRM Server for Protected Streaming不是必需的），则必须配置commons-logging以使用Log4J。

服务器可选地使用平台特定库(Microsoft Windows上的[!DNL jsafe.dll]或Linux上的[!DNL libjsafe.so]以获得最佳性能。 您可以将平台的相应库从&#x200B;[!DNL thirdparty/cryptoj/]*platform*&#x200B;复制到由Linux上的`PATH`环境变量或`LD_LIBRARY_PATH`指定的位置。

>[!NOTE]
>
>仅当操作系统和JDK都支持64位时，才应使用64位版本。 否则，您需要使用32位版本。

