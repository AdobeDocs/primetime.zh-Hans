---
description: 302重定向优化可将302个重定向响应的数量减至最少，这使您的应用程序能够更有效地平衡负载。
title: HTTP 302重定向优化
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---


# HTTP 302重定向优化{#http-redirect-optimization}

302重定向优化可将302个重定向响应的数量减至最少，这使您的应用程序能够更有效地平衡负载。

如果重定向主清单请求，并且您的播放器中启用了302优化，则从该清单对资产发出的后续请求将使用最终的域位置，从而避免额外的302个响应。

默认情况下，此功能处于禁用状态，您可以更改此设置。

如果启用此功能，则仅当以下条件的&#x200B;*all*&#x200B;为true时，才能正确使用；否则，不会进行重定向优化，并且会继续进行302个响应：

* 您的应用程序已使用`-swf-version` 21或更高版本编译为Adobe Flash Player 11.8。
* 您的最终用户已安装Adobe Flash Player 11.8或更高版本。

>[!IMPORTANT]
>
>要确保Cookie与广告请求一起传递，请禁用302重定向。 启用302重定向后，广告请求可能会被重定向到不同于Cookie所发起域的域。

## 禁用或启用302重定向优化{#section_D6687FC44C61446F878008B629A5FA19}

使用`useRedirectedUrl`属性打开(true)或关闭(false)302重定向。

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

