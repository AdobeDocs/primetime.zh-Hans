---
description: 302重定向优化可最大限度地减少302个重定向响应的数量，从而使您的应用程序可以更有效地进行负载平衡。
title: HTTP 302重定向优化
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# HTTP 302重定向优化{#http-redirect-optimization}

302重定向优化可最大限度地减少302个重定向响应的数量，从而使您的应用程序可以更有效地进行负载平衡。

如果重定向主清单请求，并且在播放器中启用了302优化，则从该清单对资产发出的后续请求将使用最终域位置，这会避免额外的302响应。

此功能默认处于禁用状态，您可以更改此设置。

如果启用此功能，则只有在 *所有* 符合以下条件：true；否则，不会发生重定向优化，并且会继续出现302个响应：

* 您的应用程序是为AdobeFlash Player11.8编译的，使用 `-swf-version` 21或更高。
* 您的最终用户安装了AdobeFlash Player11.8或更高版本。

>[!IMPORTANT]
>
>要确保随广告请求传递Cookie，请禁用302重定向。 启用302重定向后，广告请求可能会被重定向到与Cookie源自的域不同的域。

## 禁用或启用302重定向优化 {#section_D6687FC44C61446F878008B629A5FA19}

使用 `useRedirectedUrl` 属性以打开(true)或关闭(false)302重定向。

<!--<a id="example_B886777252B745AAB48B1FCC42C97A25"></a>-->

例如：

```
// Set useRedirectedUrl property to true 
var networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = true; 
  
//Set NetworkConfiguration as Metadata: 
var result:Metadata = new Metadata(); 
result.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                   networkConfiguration); 
  
var mediaResource = new MediaResource( url, MediaResourceType.HLS, result); 
  
// load the resource 
mediaPlayer.replaceCurrentResource( mediaResource, mediaPlayerItemConfig );
```
