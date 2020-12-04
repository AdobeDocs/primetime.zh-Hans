---
description: 在您的应用程序中使用Browser TVSDK提供的Browserify库文件，以使用UI-Framework创建与Browserify兼容的播放器。
seo-description: 在您的应用程序中使用Browser TVSDK提供的Browserify库文件，以使用UI-Framework创建与Browserify兼容的播放器。
seo-title: 使用UI-Framework创建与浏览器兼容的播放器
title: 使用UI-Framework创建与浏览器兼容的播放器
uuid: 544fd872-5ca1-417d-8aab-69613caada0e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 使用UI-Framework {#create-a-browserify-compatible-player-using-the-ui-framework}创建与浏览器兼容的播放器

在您的应用程序中使用Browser TVSDK提供的Browserify库文件，以使用UI-Framework创建与Browserify兼容的播放器。

TVSDK中包含的示例浏览器ify文件：

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

要使用UI-Framework创建与Browserify兼容的应用程序，必须在应用程序代码中`require`两个Browserify模块（由Browser TVSDK提供）:

1. 需要浏览器验证模块：

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. 按照[](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md)中的说明继续开发。
>您现在可以使用Browserify捆绑应用程序文件。
