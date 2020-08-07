---
seo-title: 构建许可证服务器
title: 构建许可证服务器
uuid: d7ca8a8f-c778-41a2-b823-93fac9ab07c5
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 构建许可证服务器 {#building-the-license-server}

参考实施许可证服务器包括用于部署许可证服务器的WAR文件。 它还包含所有许可证服务器源代码和Ant构建脚本(参考Implementation\Server\refimpl\build-refimpl.xml)，因此您可以轻松地更改代码。

>[!NOTE]
>
>仅当要修改源代码时，才需要此步骤。 为便于评估，您可以跳过此步骤，按装运的方式使用WAR文件。

在运行Ant脚本之前，修改脚本以指定Adobe访问SDK、Tomcat、MySQL和Log4J的位置。 在文本编辑器中打开build-refimpl.xml并编辑属性值 `sdkdir, tomcatdir, mysqldir, and log4jdir`。 要编译源代码并创建WAR文件以用于参考实现，请在包含Ant脚本 `ant -f build-refimpl.xml all` 的目录中运行脚本。 脚本完成后，将创 [!DNL refimpl-build/wars] 建包含服务器WAR文件的目录。
