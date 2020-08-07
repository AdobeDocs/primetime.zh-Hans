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

用于受保护流的Primetime DRM Server包含 [!DNL flashaccesserver.war]。 如果您：

* 要部署此WAR文件，您需要将其复制到Tomcat的目 [!DNL webapps] 录。
* 以前已部署WAR文件，您可能需要删除未打包的WAR目 [!DNL flashaccessserver] 录(在Tomcat的目 [!DNL webapps] 录中)。

* 要阻止Tomcat解包WAR文件，请在Tomcat的 [!DNL server.xml] 目录中编辑该文 [!DNL conf] 件，并通过将 `unpackWARs` 其设置为来配置该属性 `false`。

>[!NOTE]
>
>如果已将Tomcat配置为 [!DNL commons-logging.jar] 包含在系统类路径中（Primetime DRM Server for Protected Streaming不需要），则必须配置共享日志以使用Log4J。

服务器可选地使用特定于平台的库( [!DNL jsafe.dll] 在Microsoft Windows或Linux上 [!DNL libjsafe.so] )以获得最佳性能。 您可以将平台的相应库从平 [!DNL thirdparty/cryptoj/]*台&#x200B;*复制到环境变量或Linux`PATH`上指定`LD_LIBRARY_PATH`的位置。

>[!NOTE]
>
>仅当操作系统和JDK都支持64位时，才应使用64位版本。 否则，您需要使用32位版本。

