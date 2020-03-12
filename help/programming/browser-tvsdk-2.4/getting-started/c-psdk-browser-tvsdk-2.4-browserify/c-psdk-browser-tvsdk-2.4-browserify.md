---
description: 您可以使用浏览器TVSDK提供的JS文件创建与浏览器兼容的播放器。
seo-description: 您可以使用浏览器TVSDK提供的JS文件创建与浏览器兼容的播放器。
seo-title: 兼容浏览器的播放器
title: 兼容浏览器的播放器
uuid: 1832c826-d5d0-41b0-852f-286c8e4fa0f3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 概述 {#browserify-compatible-player-overview}

您可以使用浏览器TVSDK提供的JS文件创建与浏览器兼容的播放器。

浏览器TVSDK提供两个与浏览器兼容的JS文件。 一种是与AdobePSDK模块一起使用；这是用于开发没有UI-Framework的应用程序。 另一个是与UI-Framework模块一起使用；它返回您使用UI-Framework编写应用程序时使用的PTP命名空间。

要开始使用Browserify，请运行以下设置命令，以在和下 [!DNL final.js] 的目录中创建文件(您的Browserify包 [!DNL example] 文件) [!DNL samples/browerify/reference][!DNL samples/browerify/ui-framework]:

1. 导航到 [!DNL samples/browserify/reference/build]。
1. 运行以下命令：

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. 导航到 [!DNL samples/browserify/ui-framework/build]。
1. 运行与步骤2中相同的命令。

完成此设置后，您可以根据随TVSDK提供的示例继续创建与Browserify兼容的TVSDK应用程序。
