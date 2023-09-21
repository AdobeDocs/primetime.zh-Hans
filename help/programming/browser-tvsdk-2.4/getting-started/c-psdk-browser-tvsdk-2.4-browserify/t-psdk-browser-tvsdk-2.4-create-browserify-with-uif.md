---
description: 使用应用程序中的浏览器TVSDK提供的浏览器库文件，通过UI-Framework创建与浏览器兼容的播放器。
title: 使用UI-Framework创建与浏览器兼容的播放器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 使用UI-Framework创建与浏览器兼容的播放器 {#create-a-browserify-compatible-player-using-the-ui-framework}

使用应用程序中的浏览器TVSDK提供的浏览器库文件，通过UI-Framework创建与浏览器兼容的播放器。

TVSDK中包含的示例浏览器文件：

* [！DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [！DNL [...]/samples/browserify/ui-framework/build/package.json]
* [！DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [！DNL [...]/samples/browserify/ui-framework/examples/sample.js]

要使用UI-Framework创建与浏览器兼容的应用程序，您必须 `require` 应用程序代码中的两个浏览器模块（由浏览器TVSDK提供）：

1. 需要浏览器模块：

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. 按照中的说明继续开发 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>您现在可以使用Browserify捆绑应用程序文件。
