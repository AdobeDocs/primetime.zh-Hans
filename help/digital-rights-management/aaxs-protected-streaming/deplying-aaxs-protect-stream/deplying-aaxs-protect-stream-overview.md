---
seo-title: 部署Adobe Access Server的受保护流概述
title: 部署Adobe Access Server的受保护流概述
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 部署Adobe Access Server的受保护流概述{#deploying-the-adobe-access-server-for-protected-streaming-overview}

在部署Adobe Access Server的受保护流之前，请确保已安装“要求”部分中列出的Java和Tomcat版本。

Adobe Access Server的受保护流软件包包括[!DNL flashaccesserver.war]。 要部署此WAR文件，请将其复制到Tomcat的[!DNL webapps]目录。 如果之前已部署WAR文件，则可能需要手动删除未打包的WAR目录（Tomcat的[!DNL webapps]目录中的[!DNL flashaccessserver]）。 要防止Tomcat解包WAR文件，请编辑Tomcat的[!DNL conf]目录中的[!DNL server.xml]文件，并将`unpackWARs`属性设置为`false`。

>[!NOTE]
>
>如果已将Tomcat配置为在系统类路径中包含[!DNL commons-logging.jar](保护流的Adobe Access Server不需要)，则必须将commons-logging配置为使用Log4J。

服务器可选地使用平台特定库（Microsoft Windows上的[!DNL jsafe.dll]或Linux上的[!DNL libjsafe.so]）以获得最佳性能。 将平台的相应库从&#x200B;[!DNL thirdparty/cryptoj/]*platform*&#x200B;复制到由`PATH`环境变量（或Linux上的`LD_LIBRARY_PATH`）指定的位置。

>[!NOTE]
>
>仅当操作系统和JDK都支持64位时，才应使用64位版本，否则应使用32位版本。

