---
description: 302重定向优化将302个重定向响应的数量降至最低，这使应用程序能够更有效地平衡负载。
seo-description: 302重定向优化将302个重定向响应的数量降至最低，这使应用程序能够更有效地平衡负载。
seo-title: HTTP 302重定向优化
title: HTTP 302重定向优化
uuid: 91ed8919-a3c1-4e57-9eaf-e3ba430de35f
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# HTTP 302重定向优化 {#http-redirect-optimization}

302重定向优化将302个重定向响应的数量降至最低，这使应用程序能够更有效地平衡负载。

如果重定向主清单请求，并且您的播放器中启用了302优化，则从该清单对资产发出的后续请求将使用最终的域位置，从而避免额外的302个响应。 此功能默认处于启用状态，您可以更改此设置。

## 禁用或启用302重定向优化 {#section_8977448B268E41D69A8F75B60EB9DA3B}

使用 `useRedirectedUrl` 属性打开()或关 `true`闭( `false`)302重定向。

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
