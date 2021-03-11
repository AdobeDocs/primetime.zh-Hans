---
description: 要使用Flash Player，请确保您的环境符合必要要求。
title: Flash Player要求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---


# Flash Player要求{#flash-player-requirements}

要使用Flash Player，请确保您的环境符合必要要求。

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

以下是Flash Player的要求：

* 要播放`Primetime.js`，请至少安装Flash Player版本23。
* 要提示更新Flash Player版本23或更高版本，请至少安装Flash Player版本11.0.0。

## 打包要求{#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

使用Flash Player播放需要以下SWF文件：

* 处理浏览器TVSDK API的主应用程序SWF文件。
* 处理Flash Player安装和更新的`playerProductInstall.swf` SWF文件。

此外，Flash中的视频播放需要授权令牌文件，该文件可能是SWF或`.DAT`文件。 可以使用AdobePSDK API指定SWF文件的路径、授权令牌文件以及令牌文件名和类型。

例如：

```js
// Set relative or http path to directory containing SWF.  
// Defaults to current directory for the html page. 
AdobePSDK.setSWFPath(<swfPath>); 
 
// Set the relative or http path to directory containing token file(s). 
// Defaults to SWFPath + "token/". 
AdobePSDK.setAuthorizationTokenPath(<authorizationTokenPath>); 
 
// Set the name of the token file, do not include any path in this string. 
AdobePSDK.setAuthorizationTokenFilename("hlsaf_localhost.swf"); 
 
//Set the token type, "DAT" or "SWF". Defaults to "DAT" 
AdobePSDK.setAuthorizationTokenType("SWF");
```

