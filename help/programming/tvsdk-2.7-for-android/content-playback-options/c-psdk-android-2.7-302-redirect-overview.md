---
description: 302重定向优化可最大限度地减少302个重定向响应的数量，从而使您的应用程序可以更有效地进行负载平衡。
title: HTTP 302重定向优化
exl-id: fdbdc2b4-6c1a-4ab1-80e2-b5e079ffa906
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# HTTP 302重定向优化 {#http-redirect-optimization}

302重定向优化可最大限度地减少302个重定向响应的数量，从而使您的应用程序可以更有效地进行负载平衡。

如果重定向主清单请求，并在播放器中启用302优化，则从该清单对资产发出的后续请求将使用最终域位置，从而避免额外302响应。 此功能默认处于启用状态，您可以更改此设置。

## 禁用或启用302重定向优化 {#section_8977448B268E41D69A8F75B60EB9DA3B}

使用 `useRedirectedUrl` 要打开302重定向的属性( `true`)或关闭( `false`)。

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
