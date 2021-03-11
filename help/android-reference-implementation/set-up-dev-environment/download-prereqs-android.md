---
title: 下载和配置必备软件
description: 安装过程很简单。 如果您的系统中已安装JDK，则可以跳过此步骤，但请注意，您的JDK、Eclipse IDE和OS需要兼容。
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# 下载并配置必备软件{#download-and-configure-prerequisite-software}

1. 从[https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/)下载JDK。

   安装过程很简单。 如果您的系统中已安装JDK，则可以跳过此步骤，但请注意，您的JDK、Eclipse IDE和OS需要兼容。
1. 从[https://www.eclipse.org/downloads](https://www.eclipse.org/downloads)下载适用于Java开发人员的Eclipse IDE。

   解压包后，您可以直接运行Eclipse。 没有安装程序。
1. 从[https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)下载Android SDK ADT Bundle。

   此捆绑包包含Eclipse。 如果您的系统中已安装Eclipse，则可以从[!UICONTROL Use An Existing IDE]部分下载适用于您的平台的SDK工具。

   拆开包装并安装到您要记住的位置。 您需要在以后的步骤中引用它。
1. 配置Android SDK。
   1. 打开终端（在Mac OS X中）或命令提示符（在Windows中）。
   1. 导航到下载/解压缩Android SDK的目录。
   1. 转到工具文件夹，该文件夹包含名为[!DNL android]的文件。
   1. 运行以下命令：

      * 对于Mac OS X/Unix:

         ```
         chmod +x android 
         android update sdk --no-ui
         ```

      * 对于Windows:

         ```
         android update sdk --no-ui
         ```

         此过程需要一段时间。

1. 配置Eclipse。
   1. 开始 Eclipse。

      在Windows上，如果Eclipse不开始，并且报告的问题是Eclipse找不到所需的Java文件，请尝试以下操作：

      * 将`-vm C:\[path to your JDK bin]\javaw.exe`添加到[!DNL eclipse.ini]文件。
   1. 选择&#x200B;**[!UICONTROL Help]** > **[!UICONTROL Install New Software]**。
   1. 单击 **[!UICONTROL Add...]**.
   1. 输入`Android`作为名称。
   1. 输入`https://dl-ssl.google.com/android/eclipse/`作为&#x200B;**[!UICONTROL Work with]**&#x200B;链接。
   1. 单击 **[!UICONTROL OK]**.

      您应当看到类似以下对话框：

      ![](assets/available_software.jpg)

   1. 选择生成的包（开发人员工具和NDK插件中的包），然后单击&#x200B;**[!UICONTROL Next]**。

      这将下载Android开发工具(ADT)。
   1. 下载完成后，重新启动Eclipse。

   Android SDK现已安装。 1.配置Eclipse，以便它能够找到Android SDK并将其用作资源。
   1. 打开Eclipse。
   1. 在Windows上选择&#x200B;**[!UICONTROL Window]** > **[!UICONTROL Preferences]**; Mac OS X上的&#x200B;**[!UICONTROL ADT]** > **[!UICONTROL Preferences]**。
   1. 选择&#x200B;**[!UICONTROL Android]**&#x200B;选项卡。
   1. 浏览至Android SDK的位置。
   1. 单击 **[!UICONTROL Apply]**.

      ![步骤结果](assets/ss2.jpg)


