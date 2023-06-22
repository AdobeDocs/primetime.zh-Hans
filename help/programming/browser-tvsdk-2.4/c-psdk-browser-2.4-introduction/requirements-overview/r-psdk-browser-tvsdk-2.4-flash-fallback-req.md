---
description: 要使用Flash Player，请确保您的环境满足必要的要求。
title: Flash Player要求
exl-id: 26531d0d-d34c-4134-8a05-0604f00a3107
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Flash Player要求{#flash-player-requirements}

要使用Flash Player，请确保您的环境满足必要的要求。

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

以下是Flash Player的要求：

* 回放 `Primetime.js`，至少安装Flash Player版本23。
* 要提示更新Flash Player版本23或更高版本，请至少安装Flash Player版本11.0.0。

## 打包要求 {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

使用Flash Player播放需要以下SWF文件：

* 处理浏览器TVSDK API的主应用程序SWF文件。
* 此 `playerProductInstall.swf` 处理Flash Player安装和更新的SWF文件。

此外，Flash中的视频播放需要授权令牌文件，该文件可能是SWF或 `.DAT` 文件。 可以使用AdobePSDK API指定SWF文件的路径、授权令牌文件以及令牌文件名和类型。

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
