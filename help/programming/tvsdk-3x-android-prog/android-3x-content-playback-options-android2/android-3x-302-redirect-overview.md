---
description: 302重定向优化可将302个重定向响应的数量减至最少，这使您的应用程序能够更有效地平衡负载。
title: HTTP 302重定向优化
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 2%

---


# HTTP 302重定向优化{#http-redirect-optimization}

302重定向优化可将302个重定向响应的数量减至最少，这使您的应用程序能够更有效地平衡负载。

如果重定向主清单请求，并且您的播放器中启用了302优化，则从该清单对资产发出的后续请求将使用最终的域位置，从而避免额外的302个响应。 此功能默认为启用状态，您可以更改此设置。

## 禁用或启用302重定向优化{#section_8977448B268E41D69A8F75B60EB9DA3B}

使用`useRedirectedUrl`属性打开(`true`)或关闭(`false`)302重定向。

<!--<a id="example_888749F70C8A43279D06A29BD68E7E4D"></a>-->

例如：

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration on MediaPlayerItemConfig 
MediaPlayerItemConfig config = new MediaPlayerItemConfig (); 
config.setNetworkConfiguration(networkConfiguration); 
 
//Use this config when loading the MediaPlayerItem or calling replaceCurrentResource
```
