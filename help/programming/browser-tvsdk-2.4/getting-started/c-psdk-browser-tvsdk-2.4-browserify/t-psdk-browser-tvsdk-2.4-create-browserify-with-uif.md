---
description: 使用应用程序中由浏览器TVSDK提供的Browserify库文件，以使用UI-Framework创建与Browserify兼容的播放器。
seo-description: 使用应用程序中由浏览器TVSDK提供的Browserify库文件，以使用UI-Framework创建与Browserify兼容的播放器。
seo-title: 使用UI-Framework创建与浏览器兼容的播放器
title: 使用UI-Framework创建与浏览器兼容的播放器
uuid: 544fd872-5ca1-417d-8aab-69613caada0e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 使用UI-Framework创建与浏览器兼容的播放器 {#create-a-browserify-compatible-player-using-the-ui-framework}

使用应用程序中由浏览器TVSDK提供的Browserify库文件，以使用UI-Framework创建与Browserify兼容的播放器。

TVSDK中包含的示例浏览器ify文件：

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

要使用UI-Framework创建与Browserify兼容的应用程序，您必须在应用程 `require` 序代码中使用两个Browserify模块（由Browser TVSDK提供）:

1. 需要Browserify模块：

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. 按照中的说明继续开发 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md)。
>您现在可以使用Browserify捆绑应用程序文件。
