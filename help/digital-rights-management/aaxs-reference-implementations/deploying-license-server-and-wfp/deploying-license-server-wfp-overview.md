---
title: 部署许可证服务器和观察文件夹打包程序概述
description: 部署许可证服务器和观察文件夹打包程序概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 部署许可证服务器和观察文件夹打包程序概述 {#deploying-the-license-server-and-watched-folder-packager-overview}

将许可证服务器WAR文件复制到Tomcat [!DNL webapps] 目录。 如果您以前部署过WAR文件，您可能需要手动删除解压缩的WAR目录( [!DNL flashaccess]， [!DNL edcws]、和 [!DNL flashaccess-packager] 在Tomcat的 [!DNL webapps] 目录)。 要防止Tomcat解压缩WAR文件，请编辑 [!DNL server.xml] 在Tomcat的conf目录中创建，并设置 `unpackWARs` 属性至 `false`.

属性文件( [!DNL flashaccess-refimpl.properties])必须在类路径上，服务器才能加载属性。 将此文件复制到目录，并使用适当的值更新该文件。 编辑 [!DNL catalina.properties] tomcat中的文件 [!DNL conf] 目录并添加包含 [!DNL flashaccess-refimpl.properties] 到 `shared.loader` 属性。 此 [!DNL log4j.xml] 用于配置日志记录的文件也必须在类路径上(请参见 [!DNL resources\log4j.xml] 例如)。

参考实施服务器使用多个证书文件、策略文件和其他资源。 这些文件全部位于一个资源文件夹中。 默认情况下，资源文件夹为 [!DNL C:\flashaccess-server-resources]，但此位置可以在以下位置修改： [!DNL flashaccess-refimpl.properties]. 在启动服务器之前，请务必将所有必需资源复制到此位置。

要启动Tomcat和许可证服务器，请运行 `catalina.bat start` 从Tomcat的 [!DNL bin] 目录。
