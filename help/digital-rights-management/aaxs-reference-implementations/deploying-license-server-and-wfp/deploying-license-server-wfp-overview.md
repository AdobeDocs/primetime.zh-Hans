---
title: 部署许可证服务器和监视文件夹打包程序概述
description: 部署许可证服务器和监视文件夹打包程序概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 部署许可证服务器和监视文件夹打包程序概述{#deploying-the-license-server-and-watched-folder-packager-overview}

将许可证服务器WAR文件复制到Tomcat的[!DNL webapps]目录。 如果之前已部署WAR文件，则可能需要手动删除未打包的WAR目录（[!DNL flashaccess]、[!DNL edcws]和Tomcat的[!DNL webapps]目录中的[!DNL flashaccess-packager]）。 要防止Tomcat解包WAR文件，请编辑Tomcat的conf目录中的[!DNL server.xml]文件，并将`unpackWARs`属性设置为`false`。

属性文件([!DNL flashaccess-refimpl.properties])必须位于类路径中，服务器才能加载属性。 将此文件复制到一个目录，并使用适当的值更新文件。 编辑Tomcat的[!DNL conf]目录中的[!DNL catalina.properties]文件，并将包含[!DNL flashaccess-refimpl.properties]的目录添加到`shared.loader`属性中。 用于配置日志记录的[!DNL log4j.xml]文件也必须位于类路径中（例如，请参见[!DNL resources\log4j.xml]）。

参考实现服务器使用多个证书文件、策略文件和其他资源。 这些文件都位于一个资源文件夹中。 默认情况下，资源文件夹为[!DNL C:\flashaccess-server-resources]，但此位置可在[!DNL flashaccess-refimpl.properties]中修改。 请务必在启动服务器之前将所有所需资源复制到此位置。

要开始Tomcat和许可证服务器，请从Tomcat的[!DNL bin]目录运行`catalina.bat start`。
