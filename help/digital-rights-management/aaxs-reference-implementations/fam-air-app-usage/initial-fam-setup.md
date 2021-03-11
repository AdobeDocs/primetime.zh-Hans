---
title: 初始Flash Access管理器设置
description: 初始Flash Access管理器设置
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 初始Flash Access管理器设置{#initial-flash-access-manager-setup}

请按照以下过程设置Flash Access管理器：

1. 部署Packager服务器。 此服务器仅应对防火墙内的用户可用（请勿在面向公共的计算机上部署此软件）。 有关部署服务器的详细信息，请参阅[部署许可证服务器和监视文件夹打包程序](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md)。

   * 将[!DNL flashaccess-packager.war]复制到Tomcat的webapps文件夹。
   * 将[!DNL flashaccess-refimpl-packager.properties]从资源复制到类路径上的位置。
   * 开始服务器。 属性文件中会出现一些错误；由于尚未填写这些物业，因此预期会出现这种情况。

1. 通过启动[!DNL .air]文件（需要AIR 1.5或更高版本）来安装Flash Access Manager AIR应用程序。
1. 启动Flash Access Manager AIR应用程序。

   如果您的服务器在`https://localhost:8080*`以外的其他位置运行，您会看到错误，表明应用程序无法连接到服务器。 关闭错误对话框，并在“首选项”选项卡中填写Packager服务器URL的正确URL。 如果服务器在指定的URL上运行，而属性文件在类路径上，则“首选项”屏幕将填充属性文件中的值。 设置Packager服务器URL后，AIR应用程序会记住此设置，您不必在下次启动应用程序时输入它。
1. 填写“首选项”选项卡中的值，然后单击&#x200B;**[!UICONTROL Save]**。
1. 如果要使用监视文件夹，则需要重新启动服务器以从步骤3中看到的错误中恢复。 如果首选项配置正确，则启动过程中不会显示任何错误。

