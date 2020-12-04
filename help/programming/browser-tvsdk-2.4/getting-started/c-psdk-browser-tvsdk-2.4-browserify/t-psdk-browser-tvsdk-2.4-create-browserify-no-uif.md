---
description: 在您的应用程序中使用Browser TVSDK提供的Browserify库文件创建与Browserify兼容的播放器。
seo-description: 在您的应用程序中使用Browser TVSDK提供的Browserify库文件创建与Browserify兼容的播放器。
seo-title: 创建不带UI-Framework的与浏览器兼容的播放器
title: 创建不带UI-Framework的与浏览器兼容的播放器
uuid: c4315bc8-c75d-4dd9-8680-946c1197be1e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 创建不带UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}的与浏览器兼容的播放器

在您的应用程序中使用Browser TVSDK提供的Browserify库文件创建与Browserify兼容的播放器。

主题[](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md)列表了通常在创建基本视频播放器时包含的浏览器TVSDK库集。 为此，您只需添加`script`标记，其属性`src`指向库。

创建与Browserify兼容的播放器的过程略有不同。 对于此，使用`require`命令将[!DNL AdobePSDK.module.js]文件（由浏览器TVSDK提供）包含在应用程序中。 此文件按照基本播放器库文件的相关顺序捆绑基本播放器库文件，并返回用于为播放器实现功能的`AdobePSDK`命名空间。

浏览器TVSDK在发行包中提供以下示例Browserify应用程序和构建文件：

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

要创建与浏览器兼容的视频播放器，请执行以下操作：

1. 需要返回`AdobePSDK`命名空间符的与Browserify兼容的库文件：

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. 按照[](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md)中的说明创建您的播放器。

   此任务中的步骤1替换基本播放器说明中的步骤，在该步骤中，您将在应用程序文件中源入各个基本播放器库。
您现在可以使用Browserify捆绑应用程序文件。
