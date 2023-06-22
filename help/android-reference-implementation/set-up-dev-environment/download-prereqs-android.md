---
title: 下载并配置必备软件
description: 安装过程简单明了。 如果您的系统上已安装了JDK，则可以跳过此步骤，但请注意，您的JDK、Eclipse IDE和操作系统需要兼容。
exl-id: c2884a55-4f5e-4da8-807d-633625d7fef9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 下载并配置必备软件 {#download-and-configure-prerequisite-software}

1. 从下载JDK [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/).

   安装过程简单明了。 如果您的系统上已安装了JDK，则可以跳过此步骤，但请注意，您的JDK、Eclipse IDE和操作系统需要兼容。
1. 从下载适用于Java开发人员的Eclipse IDE [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads).

   解压缩包后，您可以直接运行Eclipse。 没有安装程序。
1. 从下载Android SDK ADT包 [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html).

   此捆绑包中包含Eclipse。 如果您的系统上已安装Eclipse，则可以从以下网站下载适用于您的平台的SDK工具： [!UICONTROL Use An Existing IDE] 部分。

   打开包装并安装到您将会记住的位置。 您需要在后续步骤中引用此内容。
1. 配置Android SDK。
   1. 打开终端(在Mac OS X中)或命令提示符（在Windows中）。
   1. 导航到下载/解压缩Android SDK的目录。
   1. 转到tools文件夹，其中包含名为的文件 [!DNL android].
   1. 运行以下命令：

      * 对于Mac OS X/Unix：

         ```
         chmod +x android 
         android update sdk --no-ui
         ```

      * 对于Windows：

         ```
         android update sdk --no-ui
         ```

         此过程需要花费一些时间。

1. 配置Eclipse。
   1. 启动Eclipse。

      在Windows上，如果Eclipse未启动，并且报告的问题是Eclipse找不到所需的Java文件，请尝试以下操作：

      * 添加 `-vm C:\[path to your JDK bin]\javaw.exe` 敬您的 [!DNL eclipse.ini] 文件。
   1. 选择  **[!UICONTROL Help]** > **[!UICONTROL Install New Software]** .
   1. 单击 **[!UICONTROL Add...]**.
   1. 输入 `Android` 名称。
   1. 输入 `https://dl-ssl.google.com/android/eclipse/` 对于 **[!UICONTROL Work with]** 链接。
   1. 单击 **[!UICONTROL OK]**.

      您应该会看到一个类似于下面的对话框：

      ![](assets/available_software.jpg)

   1. 选择生成的包（开发人员工具和NDK插件中的包）并单击 **[!UICONTROL Next]**.

      这将下载Android开发工具(ADT)。
   1. 下载完成后，重新启动Eclipse。

   Android SDK现已安装。 1.配置Eclipse，以便能够找到Android SDK并将其用作资源。
   1. 打开Eclipse。
   1. 选择  **[!UICONTROL Window]** > **[!UICONTROL Preferences]** 在Windows上；  **[!UICONTROL ADT]** > **[!UICONTROL Preferences]** 在Mac OS X上。
   1. 选择 **[!UICONTROL Android]** 选项卡。
   1. 浏览到Android SDK的位置。
   1. 单击 **[!UICONTROL Apply]**.

      ![步骤结果](assets/ss2.jpg)
