---
description: 302重定向优化将302个重定向响应的数量降至最低，这使您的应用程序能够更有效地平衡负载。
seo-description: 302重定向优化将302个重定向响应的数量降至最低，这使您的应用程序能够更有效地平衡负载。
seo-title: HTTP 302重定向优化
title: HTTP 302重定向优化
uuid: d3009c6c-320a-4c0f-b6ba-bf6473049823
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# HTTP 302重定向优化{#http-redirect-optimization}

302重定向优化将302个重定向响应的数量降至最低，这使您的应用程序能够更有效地平衡负载。

如果重定向主清单请求，并且您的播放器中启用了302优化，则从该清单对资产发出的后续请求将使用最终的域位置，从而避免额外的302个响应。 此功能在默认情况下处于启用状态，您可以更改此设置。

>[!IMPORTANT]
>
>此功能仅在支持`XMLHttpRequest`对象中`responseURL`属性的认证浏览器中受支持。

对于Flash回退，请记住以下信息：

* 您的最终用户必须安装AdobeFlash Player版本23或更高版本。
* 如果禁用流完整性，则仅认证的浏览器支持302重定向。

## 禁用302重定向优化{#disabling-redirect-optimization}

您可以使用useRedirectedUrl属性启用302重定向(true)或禁用(false)。

例如：

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
