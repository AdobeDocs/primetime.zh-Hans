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


# 部署Adobe Access Server的受保护流概述 {#deploying-the-adobe-access-server-for-protected-streaming-overview}

在部署Adobe Access Server的受保护流之前，请确保已安装“要求”部分中列出的Java和Tomcat版本。

Adobe Access Server的受保护流软件包包括 [!DNL flashaccesserver.war]。 要部署此WAR文件，请将其复制到Tomcat的目 [!DNL webapps] 录。 如果之前已部署WAR文件，则可能需要手动删除未打包的WAR目 [!DNL flashaccessserver] 录(在Tomcat的目 [!DNL webapps] 录中)。 要防止Tomcat解包WAR文件，请在Tomcat的 [!DNL server.xml] 目录中编辑该文 [!DNL conf] 件，并将属 `unpackWARs` 性设置为 `false`。

>[!NOTE]
>
>如果已将Tomcat配置为 [!DNL commons-logging.jar] 在系统类路径中包含(保护流的Adobe Access Server不要求)，则必须将commons-logging配置为使用Log4J。

服务器可选地使用特定于平台的库( [!DNL jsafe.dll] 在Microsoft Windows或Linux [!DNL libjsafe.so] 上)以获得最佳性能。 将平台的相应库从平 [!DNL thirdparty/cryptoj/]*台&#x200B;*复制到环境变量(或`PATH`在Linux上`LD_LIBRARY_PATH`)指定的位置。

>[!NOTE]
>
>仅当操作系统和JDK都支持64位时，才应使用64位版本，否则应使用32位版本。

