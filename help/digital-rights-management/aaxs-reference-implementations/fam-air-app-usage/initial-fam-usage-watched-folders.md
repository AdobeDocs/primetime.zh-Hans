---
title: 观察文件夹
description: 观察文件夹
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 观察文件夹 {#watched-folders}

您可以使用Watched文件夹自动打包在特定文件夹中创建的内容。 每个观察文件夹都可以配置不同的包装选项。 要在创建Watched文件夹之前测试打包选项，请使用“Package Media（打包介质）”选项卡。

要创建Watched文件夹，请单击 **[!UICONTROL Add New Watched Folder]** 并填写打包选项。 请参阅 [正在打包媒体文件](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md) 部分以了解每个选项的描述。 完成后，单击 **[!UICONTROL Save Watched Folder Properties]**.

保存Watched文件夹后，打包选项将保存到 *[输入文件夹]* [!DNL \properties\watchfolder.properties]. 任何添加到输入文件夹的内容，只要符合“输入媒体文件选择”标准，就会自动打包并置于“输出文件夹”中。 请参阅部分中的全局Watched文件夹首选项 [Packager首选项](../../aaxs-reference-implementations/fam-air-app-usage/initial-fam-setup-set-prefs/initial-fam-setup-pkg-prefs.md) 配置其他观察文件夹选项。

要修改Watched文件夹设置，请从屏幕顶部的列表中选择Watched文件夹输入路径。 修改设置并单击 **[!UICONTROL Save Watched Folder Properties]**.

要删除观察文件夹，请从屏幕顶部的列表中选择观察文件夹输入路径，然后单击 **[!UICONTROL Delete Watched Folder Properties]**.
