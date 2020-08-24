---
description: 'null'
seo-description: 'null'
seo-title: 初始Flash Access管理器设置
title: 初始Flash Access管理器设置
uuid: e9041f7c-b098-4121-88bf-ff3e6369e01b
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---


# 初始Flash Access管理器设置 {#initial-flash-access-manager-setup}

请按照以下过程设置Flash Access管理器：

1. 部署Packager服务器。 此服务器应仅对防火墙内的用户可用（请勿在面向公共的计算机上部署此软件）。 有关部署服务器的详细信息，请参 [阅部署许可证服务器和监视文件夹打包程序](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md)。

   * 复 [!DNL flashaccess-packager.war] 制到Tomcat的Webapps文件夹。
   * 从资 [!DNL flashaccess-refimpl-packager.properties] 源复制到类路径上的位置。
   * 开始服务器。 属性文件中会出现一些错误；由于尚未填写这些属性，因此需要填写此字段。

1. 通过启动文件(需要AIR 1.5 [!DNL .air] 或更高版本)安装Flash Access管理器AIR应用程序。
1. 启动Flash Access管理器AIR应用程序。

   如果服务器在其他位置运行， `https://localhost:8080*`您会看到错误，表明应用程序无法连接到服务器。 关闭错误对话框，并在“首选项”选项卡中填写Packager Server URL的正确URL。 如果服务器在指定的URL上运行，并且属性文件在类路径中，则“首选项”屏幕将填充属性文件中的值。 设置打包程序服务器URL后，AIR应用程序会记住此设置，您不必在下次启动应用程序时输入它。
1. 填写“首选项”选项卡中的值，然后单击 **[!UICONTROL Save]**。
1. 如果要使用“监视文件夹”，您需要重新启动服务器以从步骤3中看到的错误中恢复。 如果首选项配置正确，则启动过程中不会显示错误。

