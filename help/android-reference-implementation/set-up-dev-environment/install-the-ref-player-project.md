---
description: 《TVSDK Primetime参考》是围绕TVSDK和AVE框架构建的Android应用程序。
seo-description: 《TVSDK Primetime参考》是围绕TVSDK和AVE框架构建的Android应用程序。
seo-title: 构建Primetime参考实施
title: 构建Primetime参考实施
uuid: ab12660a-1563-49a4-82d9-1ab13f8a92be
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 构建Primetime参考实施 {#build-the-primetime-reference-implementation}

《TVSDK Primetime参考》是围绕TVSDK和AVE框架构建的Android应用程序。

在Eclipse中设置和构建Primetime参考项目：

1. 下载TVSDK Android zip文件，并将其解压缩到您将记住的某个位置的目录中。
1. 启动Eclipse。
1. 选择 **[!UICONTROL File]** > **[!UICONTROL Import]**。
1. 选择 **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**。
1. 单击 **[!UICONTROL Next]**.
1. 使用 **[!UICONTROL Browse]** 按钮将字段填 **[!UICONTROL Root Directory]** 充到解压缩TVSDK Android zip文件 [!DNL samples/PrimetimeReference/src] 时所在的目录。
1. 选择要导入的以下项目： **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**。
1. 单击 **[!UICONTROL Finish]**.
1. 选择 **[!UICONTROL Project]** > **[!UICONTROL Build Project]** 以构建项目。

   如果将项目设置为自动构建，则不需要此步骤。
1. 如果要将测试项目包含在工作区中，请将测试项目与PrimetimeReference项目关联：
   1. 重复步骤3。 到6
   1. 选择要导入的以下项目： `PrimetimeReference\tests`.
   1. 单击 **[!UICONTROL Finish]**.

      测试项目与CatalogActivity项目有依赖关系，因此您需要将测试项目与CatalogActivity项目关联。
   1. 右键单击 **[!UICONTROL tests]** 并选择 **[!UICONTROL Properties]**。
   1. 选择“ **[!UICONTROL Projects]** Java构建路径”下的选项卡。
   1. 单击 **[!UICONTROL Add...]**
   1. 选择CatalogActivity。
   1. 单击 **[!UICONTROL OK]** 以添加项目。
   1. 单击 **[!UICONTROL OK]** 以退出“属性”页面。
   1. 选择 **[!UICONTROL Project]** > **[!UICONTROL Build Project]** 以构建项目。

      如果将项目设置为自动构建，则不需要此步骤。
