---
title: 部署Adobe Access Server for Protected Streaming概述
description: 部署Adobe Access Server for Protected Streaming概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 部署Adobe Access Server for Protected Streaming概述 {#deploying-the-adobe-access-server-for-protected-streaming-overview}

在部署Adobe Access Server for Protected Streaming之前，请确保您已安装了“要求”部分中列出的Java和Tomcat版本。

适用于受保护流的Adobe Access Server包包括 [!DNL flashaccesserver.war]. 要部署此WAR文件，请将其复制到Tomcat [!DNL webapps] 目录。 如果以前部署过WAR文件，您可能需要手动删除解压缩的WAR目录( [!DNL flashaccessserver] 在Tomcat的 [!DNL webapps] 目录)。 要防止Tomcat解压缩WAR文件，请编辑 [!DNL server.xml] tomcat中的文件 [!DNL conf] 目录并设置 `unpackWARs` 属性至 `false`.

>[!NOTE]
>
>如果已将Tomcat配置为包含 [!DNL commons-logging.jar] 在System类路径上(Protected Streaming的Adobe Access Server不需要)， commons-logging必须配置为使用Log4J。

服务器可以选择使用特定于平台的库( [!DNL jsafe.dll] 在Microsoft Windows上或 [!DNL libjsafe.so] （在Linux上）以获得最佳性能。 从复制适用于您的平台的库 [!DNL thirdparty/cryptoj/]*平台* 到指定的位置 `PATH` 环境变量(或 `LD_LIBRARY_PATH` 在Linux上)。

>[!NOTE]
>
>仅当操作系统和JDK都支持64位时，才应使用64位版本，否则应使用32位版本。
