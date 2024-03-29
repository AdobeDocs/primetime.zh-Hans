---
description: 使用应用程序中浏览器TVSDK提供的浏览器库文件，创建与浏览器兼容的播放器。
title: 创建不带UI-Framework的浏览器兼容播放器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 创建不带UI-Framework的浏览器兼容播放器{#create-a-browserify-compatible-player-without-the-ui-framework}

使用应用程序中浏览器TVSDK提供的浏览器库文件，创建与浏览器兼容的播放器。

主题 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) 列出在创建基本视频播放器时通常包含的一组浏览器TVSDK库。 要执行此操作，您只需添加 `script` 标记位置 `src` 指向库的属性。

创建与Browserify兼容的播放器的过程略有不同。 为此，请使用 `require` 命令以包含 [!DNL AdobePSDK.module.js] 文件（由浏览器TVSDK提供）。 此文件将按照基本播放器库文件的正确依赖顺序捆绑这些文件，并返回 `AdobePSDK` 用于为播放器实施功能的命名空间。

浏览器TVSDK在发行版软件包中提供以下示例浏览器应用程序和生成文件：

* [！DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [！DNL [...]/samples/browserify/reference/build/package.json]
* [！DNL [...]/samples/browserify/reference/examples/sample.html]
* [！DNL [...]/samples/browserify/reference/examples/sample.js]

要创建与Browserify兼容的视频播放器：

1. 需要可返回 `AdobePSDK` 命名空间：

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. 按照中的说明创建您的播放器 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   此任务中的步骤1取代了基本播放器说明中的步骤，在该步骤中，您可以在应用程序文件中提供各个基本播放器库。
您现在可以使用Browserify捆绑应用程序文件。
