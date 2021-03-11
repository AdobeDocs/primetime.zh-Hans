---
title: 构建许可证服务器
description: 构建许可证服务器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 构建许可证服务器{#building-the-license-server}

参考实施许可证服务器包括用于部署许可证服务器的WAR文件。 它还包含所有许可证服务器源代码和Ant构建脚本(参考Implementation\Server\refimpl\build-refimpl.xml)，因此您可以轻松更改代码。

>[!NOTE]
>
>仅当要修改源代码时才需要此步骤。 出于评估目的，您可以跳过此步骤，使用发运的WAR文件。

在运行Ant脚本之前，请修改脚本以指定Adobe Access SDK、Tomcat、MySQL和Log4J的位置。 在文本编辑器中打开build-refimpl.xml，并编辑属性`sdkdir, tomcatdir, mysqldir, and log4jdir`的值。 要编译源代码并创建用于参考实现的WAR文件，请使用包含Ant脚本的目录中的`ant -f build-refimpl.xml all`运行脚本。 脚本完成后，将创建一个[!DNL refimpl-build/wars]目录，其中包含服务器WAR文件。
