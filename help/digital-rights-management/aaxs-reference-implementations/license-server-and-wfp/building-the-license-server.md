---
title: 构建许可证服务器
description: 构建许可证服务器
copied-description: true
exl-id: 0535f1e4-9f63-47a0-b55c-45c32ba0d15e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 构建许可证服务器 {#building-the-license-server}

参考实施许可证服务器包括用于部署许可证服务器的WAR文件。 它还包含所有许可证服务器源代码和Ant构建脚本(参考Implementation\Server\refimpl\build-refimpl.xml)，因此您可以轻松地更改代码。

>[!NOTE]
>
>只有在要修改源代码时，才需要执行此步骤。 出于评估目的，您可以跳过此步骤，使用随附的WAR文件。

在运行Ant脚本之前，请修改该脚本以指定AdobeAccess SDK、Tomcat、MySQL和Log4J的位置。 在文本编辑器中打开build-refimpl.xml并编辑属性的值 `sdkdir, tomcatdir, mysqldir, and log4jdir`. 要编译源代码并创建用于参考实施的WAR文件，请使用以下命令运行脚本： `ant -f build-refimpl.xml all` 在包含Ant脚本的目录中。 脚本完成后， [!DNL refimpl-build/wars] 将创建包含服务器WAR文件的目录。
