---
seo-title: 部署Adobe Primetime DRM Server，实现受保护的流
title: 部署Adobe Primetime DRM Server，实现受保护的流
uuid: 83ef8237-0026-4677-b42b-ea4b6de19630
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 部署Adobe Primetime DRM Server，实现受保护的流{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

在部署Adobe Primetime DRM Server以用于受保护的流之前，必须已经安装了“要求”主题中列出的Java和Tomcat版本。

Primetime DRM Server for Protected Streaming包含 [!DNL flashaccesserver.war]。 如果您：

* 要部署此WAR文件，您需要将其复制到Tomcat的目 [!DNL webapps] 录。
* 以前已部署WAR文件，您可能需要删除解压缩的WAR目录( [!DNL flashaccessserver] 在Tomcat的目录 [!DNL webapps] 中)。

* 要阻止Tomcat解包WAR文件，请在Tomcat的目 [!DNL server.xml] 录中编辑该文件，并将 [!DNL conf] 其设置为 `unpackWARs` 以配置该属性 `false`。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>如果已将Tomcat配置为包含在系统类路径中( [!DNL commons-logging.jar] Primetime DRM Server的受保护流不需要)，则必须配置commons-logging才能使用Log4J。

服务器可选地使用特定于平台的库( [!DNL jsafe.dll] 在Microsoft Windows上或在Linux [!DNL libjsafe.so] 上)以获得最佳性能。 您可以将平台的相应库从平台复 [!DNL thirdparty/cryptoj/]*制到由环境变量指定的位&#x200B;*置或在Linux上`PATH``LD_LIBRARY_PATH`复制到该位置。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>仅当操作系统和JDK都支持64位时，才应使用64位版本。 否则，您需要使用32位版本。

