---
description: 302重定向优化可最大限度地减少302个重定向响应的数量，从而使您的应用程序可以更有效地进行负载平衡。
title: HTTP 302重定向优化
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# HTTP 302重定向优化 {#http-redirect-optimization}

302重定向优化可最大限度地减少302个重定向响应的数量，从而使您的应用程序可以更有效地进行负载平衡。

如果重定向主清单请求，并且在播放器中启用了302优化，则从该清单对资产发出的后续请求将使用最终域位置，这会避免额外的302响应。 此功能默认处于启用状态，您可以更改此设置。

>[!IMPORTANT]
>
>只有支持以下内容的认证浏览器才支持此功能： `responseURL` 中的属性 `XMLHttpRequest` 对象。

对于Flash回退，请记住以下信息：

* 最终用户必须安装AdobeFlash Player版本23或更高版本。
* 如果禁用了流完整性，则仅在认证的浏览器上支持302重定向。

## 禁用302重定向优化 {#disabling-redirect-optimization}

可以使用useRedirectedUrl属性启用302重定向(true)或禁用(false)。

例如：

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
