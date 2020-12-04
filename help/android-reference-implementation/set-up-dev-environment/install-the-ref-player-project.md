---
description: TVSDK Primetime参考是一个基于TVSDK和AVE框架构建的Android应用程序。
seo-description: TVSDK Primetime参考是一个基于TVSDK和AVE框架构建的Android应用程序。
seo-title: 构建Primetime参考实施
title: 构建Primetime参考实施
uuid: ab12660a-1563-49a4-82d9-1ab13f8a92be
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---


# 构建Primetime参考实施{#build-the-primetime-reference-implementation}

TVSDK Primetime参考是一个基于TVSDK和AVE框架构建的Android应用程序。

在Eclipse中设置和构建Primetime参考项目：

1. 下载TVSDK Android zip文件，并将其解压缩到您会记住的目录中。
1. 启动Eclipse。
1. 选择&#x200B;**[!UICONTROL File]** > **[!UICONTROL Import]**。
1. 选择&#x200B;**[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**。
1. 单击 **[!UICONTROL Next]**.
1. 使用&#x200B;**[!UICONTROL Browse]**&#x200B;按钮将&#x200B;**[!UICONTROL Root Directory]**&#x200B;字段填入[!DNL samples/PrimetimeReference/src]下的目录，您将TVSDK Android压缩文件解压缩到该目录下。
1. 选择要导入的以下项目：**[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**。
1. 单击 **[!UICONTROL Finish]**.
1. 选择&#x200B;**[!UICONTROL Project]** > **[!UICONTROL Build Project]**&#x200B;以构建项目。

   如果项目设置为自动构建，则不必执行此步骤。
1. 如果要将测试项目包含在工作区中，请将测试项目与PrimetimeReference项目关联：
   1. 重复步骤3。 到6。
   1. 选择要导入的以下项目：`PrimetimeReference\tests`。
   1. 单击 **[!UICONTROL Finish]**.

      测试项目与CatalogActivity项目有依赖关系，因此您需要将测试项目与CatalogActivity项目关联。
   1. 右键单击&#x200B;**[!UICONTROL tests]**&#x200B;并选择&#x200B;**[!UICONTROL Properties]**。
   1. 选择“Java Build Path”下的&#x200B;**[!UICONTROL Projects]**&#x200B;选项卡。
   1. 单击 **[!UICONTROL Add...]**
   1. 选择CatalogActivity。
   1. 单击&#x200B;**[!UICONTROL OK]**&#x200B;添加项目。
   1. 单击&#x200B;**[!UICONTROL OK]**&#x200B;退出“属性”页面。
   1. 选择&#x200B;**[!UICONTROL Project]** > **[!UICONTROL Build Project]**&#x200B;以构建项目。

      如果项目设置为自动构建，则不必执行此步骤。
