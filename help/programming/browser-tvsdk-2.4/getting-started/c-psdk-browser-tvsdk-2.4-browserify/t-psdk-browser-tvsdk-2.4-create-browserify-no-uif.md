---
description: 使用您的应用程序中由Browser TVSDK提供的Browserify库文件创建与Browserify兼容的播放器。
title: 创建不使用UI-Framework的与浏览器兼容的播放器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# 创建一个不带UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}的与浏览器兼容的播放器

使用您的应用程序中由Browser TVSDK提供的Browserify库文件创建与Browserify兼容的播放器。

主题[](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md)列表了通常在创建基本视频播放器时包含的浏览器TVSDK库集。 为此，只需添加`script`标签，并添加指向库的`src`属性。

创建与Browserify兼容的播放器的过程略有不同。 对于此，使用`require`命令将[!DNL AdobePSDK.module.js]文件（由Browser TVSDK提供）包含在应用程序中。 此文件以基本播放器库文件的适当依赖顺序捆绑基本播放器库文件，并返回用于实现播放器功能的`AdobePSDK`命名空间。

浏览器TVSDK在发行包中提供以下示例Browserify应用程序和构建文件：

* [!DNL [..]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/reference/build/package.json]
* [!DNL [..]/samples/browserify/reference/examples/sample.html]
* [!DNL [..]/samples/browserify/reference/examples/sample.js]

要创建与Browserify兼容的视频播放器，请执行以下操作：

1. 需要返回`AdobePSDK`命名空间的与Browserify兼容的库文件：

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. 按照[](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md)中的说明创建播放器。

   此任务中的步骤1替换了基本播放器说明中的步骤，在基本播放器说明中，您在应用程序文件中源入各个基本播放器库。
您现在可以使用Browserify捆绑应用程序文件。
