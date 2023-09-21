---
description: 您可以使用浏览器TVSDK提供的JS文件创建与浏览器兼容的播放器。
title: 浏览器兼容的播放器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概述 {#browserify-compatible-player-overview}

您可以使用浏览器TVSDK提供的JS文件创建与浏览器兼容的播放器。

浏览器TVSDK提供两个与浏览器兼容的JS文件。 一种是用于AdobePSDK模块；这用于开发没有UI-Framework的应用程序。 另一个用于UI-Framework模块；它返回使用UI-Framework编写应用程序时使用的PTP命名空间。

要开始使用Browserify，请运行以下设置命令以创建 [!DNL final.js] 文件（您的Browserify包文件） [!DNL example] 目录在 [!DNL samples/browerify/reference] 和 [!DNL samples/browerify/ui-framework]：

1. 导航到 [!DNL samples/browserify/reference/build].
1. 运行以下命令：

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. 导航到 [!DNL samples/browserify/ui-framework/build].
1. 运行与步骤2中相同的命令。

完成此设置后，您可以根据TVSDK提供的示例继续创建与浏览器兼容的TVSDK应用程序。
