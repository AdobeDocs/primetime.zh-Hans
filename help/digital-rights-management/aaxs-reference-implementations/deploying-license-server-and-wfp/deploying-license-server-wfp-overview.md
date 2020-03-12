---
seo-title: 部署许可证服务器和监视文件夹打包程序概述
title: 部署许可证服务器和监视文件夹打包程序概述
uuid: 4b71f2f4-f971-4382-ae41-171f7dfdfe21
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 部署许可证服务器和监视文件夹打包程序概述 {#deploying-the-license-server-and-watched-folder-packager-overview}

将许可证服务器WAR文件复制到Tomcat的目 [!DNL webapps] 录。 如果之前已部署WAR文件，则可能需要手动删除解压缩的WAR目录( [!DNL flashaccess]、 [!DNL edcws]和 [!DNL flashaccess-packager] Tomcat的目录 [!DNL webapps] 中)。 要防止Tomcat解包WAR文件，请在Tomcat的 [!DNL server.xml] conf目录中编辑该文件，并将该属 `unpackWARs` 性设置为 `false`。

属性文件( [!DNL flashaccess-refimpl.properties])必须位于类路径上，服务器才能加载属性。 将此文件复制到一个目录中，并使用相应的值更新文件。 编辑 [!DNL catalina.properties] Tomcat目录中的文件， [!DNL conf] 并将包含该目录的 [!DNL flashaccess-refimpl.properties] 目录添加到属 `shared.loader` 性。 用于 [!DNL log4j.xml] 配置日志记录的文件还必须位于类路径中( [!DNL resources\log4j.xml] 请参阅示例)。

参考实现服务器使用多个证书文件、策略文件和其他资源。 这些文件都位于一个资源文件夹中。 默认情况下，资源文件夹为 [!DNL C:\flashaccess-server-resources]，但此位置可在中修改 [!DNL flashaccess-refimpl.properties]。 请务必在启动服务器之前将所有必需的资源复制到此位置。

要启动Tomcat和许可证服务器，请从Tomcat `catalina.bat start` 的目录中运 [!DNL bin] 行。
