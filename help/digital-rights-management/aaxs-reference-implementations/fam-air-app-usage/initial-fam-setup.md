---
title: 初始Flash Access管理器设置
description: 初始Flash Access管理器设置
copied-description: true
exl-id: 880822f3-0d21-42fc-889e-7375a2aab11a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 初始Flash Access管理器设置 {#initial-flash-access-manager-setup}

请按下列步骤设置Flash Access管理器：

1. 部署Packager服务器。 此服务器应该仅对防火墙内的用户可用（不要在面向公众的计算机上部署此软件）。 有关部署服务器的详细信息，请参见 [部署许可证服务器和观察文件夹打包程序](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * 复制 [!DNL flashaccess-packager.war] 到Tomcat的webapps文件夹。
   * 复制 [!DNL flashaccess-refimpl-packager.properties] 从资源到类路径上的某个位置。
   * 启动服务器。 由于属性文件中的问题，您将看到一些错误；由于属性尚未填写，这是正常情况。

1. Flash Access AIR通过启动 [!DNL .air] 文件(需要AIR 1.5或更高版本)。
1. 启动Flash Access管理器AIR应用程序。

   如果您的服务器运行在 `https://localhost:8080*`，您会看到指示应用程序无法连接到服务器的错误。 关闭错误对话框，然后在“首选项”选项卡中填写Packager服务器URL的正确URL。 如果服务器在指定的URL上运行，并且属性文件位于类路径上，则“首选项”屏幕将使用属性文件中的值填充。 在设置Packager服务器URL后，AIR应用程序会记住此设置，并且下次启动应用程序时不必输入它。
1. 在“首选项”选项卡中填写值并单击 **[!UICONTROL Save]**.
1. 如果要使用Watched文件夹，则需要重新启动服务器以从您在步骤3中看到的错误中恢复。 如果首选项配置正确，则启动期间不会显示任何错误。
