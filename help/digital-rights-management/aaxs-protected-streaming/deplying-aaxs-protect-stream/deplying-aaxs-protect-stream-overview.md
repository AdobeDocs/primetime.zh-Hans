---
seo-title: 部署Adobe Access Server以实现受保护的流概述
title: 部署Adobe Access Server以实现受保护的流概述
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 部署Adobe Access Server以实现受保护的流概述 {#deploying-the-adobe-access-server-for-protected-streaming-overview}

在部署Adobe Access Server以进行受保护的流化之前，请确保已安装“要求”部分中列出的Java和Tomcat版本。

Adobe Access Server for Protected Streaming包中包括 [!DNL flashaccesserver.war]。 要部署此WAR文件，请将其复制到Tomcat的目 [!DNL webapps] 录。 如果之前已部署WAR文件，则可能需要手动删除解压缩的WAR目录( [!DNL flashaccessserver] 在Tomcat的目录 [!DNL webapps] 中)。 要防止Tomcat解包WAR文件，请在Tomcat的目 [!DNL server.xml] 录中编辑该文件， [!DNL conf] 并将属性 `unpackWARs` 设置为 `false`。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>如果已将Tomcat配置为包含在系统类路径中( [!DNL commons-logging.jar] Adobe Access Server的受保护流不是必需的)，则必须将commons-logging配置为使用Log4J。

服务器可选地使用特定于平台的库( [!DNL jsafe.dll] 在Microsoft Windows或Linux上)来 [!DNL libjsafe.so] 实现最佳性能。 将平台的相应库从平台复 [!DNL thirdparty/cryptoj/]*制到&#x200B;*（或在Linux上）由环境`PATH`变量指定的位`LD_LIBRARY_PATH`置中。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>仅当操作系统和JDK都支持64位时，才应使用64位版本，否则应使用32位版本。

