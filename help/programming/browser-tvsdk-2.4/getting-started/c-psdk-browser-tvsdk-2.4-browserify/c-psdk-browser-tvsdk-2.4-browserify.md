---
description: 您可以使用浏览器TVSDK提供的JS文件创建与浏览器兼容的播放器。
title: 浏览器兼容的播放器
exl-id: 3e9751d8-7a7e-465b-8d46-d07e4ccb1f5b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概述 {#browserify-compatible-player-overview}

您可以使用浏览器TVSDK提供的JS文件创建与浏览器兼容的播放器。

浏览器TVSDK提供两个与浏览器兼容的JS文件。 一个用于AdobePSDK模块；这用于开发没有UI-Framework的应用程序。 另一个用于UI-Framework模块；它返回使用UI-Framework编写应用程序时使用的PTP命名空间。

要开始使用Browserify，请运行以下设置命令以创建 [!DNL final.js] 文件（您的浏览器包文件） [!DNL example] 目录在 [!DNL samples/browerify/reference] 和 [!DNL samples/browerify/ui-framework]：

1. 导航到 [!DNL samples/browserify/reference/build].
1. 运行以下命令：

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. 导航到 [!DNL samples/browserify/ui-framework/build].
1. 运行与步骤2中相同的命令。

完成此设置后，您可以根据TVSDK提供的示例继续创建与浏览器兼容的TVSDK应用程序。
