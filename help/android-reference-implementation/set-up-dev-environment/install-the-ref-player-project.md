---
description: TVSDK Primetime参考是一个围绕TVSDK和AVE框架构建的Android应用程序。
title: 构建Primetime引用实施
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 构建Primetime引用实施 {#build-the-primetime-reference-implementation}

TVSDK Primetime参考是一个围绕TVSDK和AVE框架构建的Android应用程序。

要在Eclipse中设置和构建Primetime参考项目，请执行以下操作：

1. 下载TVSDK Android zip文件，并将其解压缩到您会记住的某个位置的目录中。
1. 启动Eclipse。
1. 选择 **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. 选择 **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. 单击 **[!UICONTROL Next]**.
1. 使用 **[!UICONTROL Browse]** 按钮以填充 **[!UICONTROL Root Directory]** 目录在下的字段 [!DNL samples/PrimetimeReference/src] 解压缩TVSDK Android zip文件的位置。
1. 选择要导入的以下项目： **[!UICONTROL appcompat]**， **[!UICONTROL PrimetimeReference]**.
1. 单击 **[!UICONTROL Finish]**.
1. 选择  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** 以构建项目。

   如果项目设置为自动生成，则不需要执行此步骤。
1. 如果要在工作区中包含测试项目，请将测试项目与PrimetimeReference项目关联：
   1. 重复步骤3。 到6。
   1. 选择要导入的以下项目： `PrimetimeReference\tests`.
   1. 单击 **[!UICONTROL Finish]**.

      测试项目与CatalogActivity项目存在依赖关系，因此您需要将测试项目与CatalogActivity项目关联。
   1. 右键单击 **[!UICONTROL tests]** 并选择 **[!UICONTROL Properties]**.
   1. 选择 **[!UICONTROL Projects]** 选项卡。
   1. 单击 **[!UICONTROL Add...]**
   1. 选择CatalogActivity。
   1. 单击 **[!UICONTROL OK]** 以添加项目。
   1. 单击 **[!UICONTROL OK]** 以退出“属性”页面。
   1. 选择  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** 以构建项目。

      如果项目设置为自动生成，则不需要执行此步骤。
