---
title: 部署Adobe Access Server for Protected Streaming概述
description: 部署Adobe Access Server for Protected Streaming概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 部署Adobe Access Server for Protected Streaming概述{#deploying-the-adobe-access-server-for-protected-streaming-overview}

在部署用于受保护流的Adobe Access Server之前，请确保已安装“要求”部分中列出的Java和Tomcat版本。

Adobe Access Server for Protected Streaming包包含[!DNL flashaccesserver.war]。 要部署此WAR文件，请将其复制到Tomcat的[!DNL webapps]目录。 如果之前已部署WAR文件，则可能需要手动删除解压缩的WAR目录（Tomcat的[!DNL webapps]目录中的[!DNL flashaccessserver]）。 要防止Tomcat解包WAR文件，请编辑Tomcat的[!DNL conf]目录中的[!DNL server.xml]文件，并将`unpackWARs`属性设置为`false`。

>[!NOTE]
>
>如果已将Tomcat配置为在系统类路径中包含[!DNL commons-logging.jar](对于受保护流的Adobe Access Server不要求)，则必须将commons-logging配置为使用Log4J。

服务器可以选择使用特定于平台的库（Microsoft Windows上的[!DNL jsafe.dll]或Linux上的[!DNL libjsafe.so]）以获得最佳性能。 将适合您的平台的库从&#x200B;[!DNL thirdparty/cryptoj/]*platform*&#x200B;复制到由`PATH`环境变量（或Linux上的`LD_LIBRARY_PATH`）指定的位置。

>[!NOTE]
>
>仅当操作系统和JDK都支持64位时，才应使用64位版本，否则应使用32位版本。

