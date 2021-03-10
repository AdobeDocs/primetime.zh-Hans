---
description: 302重定向优化可将302个重定向响应的数量减至最少，这使您的应用程序能够更有效地平衡负载。
title: 禁用或启用302重定向优化
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 1%

---


# HTTP 302重定向优化{#http-302-redirect-optimization}

302重定向优化可将302个重定向响应的数量减至最少，这使您的应用程序能够更有效地平衡负载。

如果重定向主清单请求，并且您的播放器中启用了302优化，则从该清单对资产发出的后续请求将使用最终的域位置，从而避免额外的302个响应。

此功能默认为启用状态，您可以更改此设置。

## 禁用或启用302重定向优化{#disable-or-enable-redirect-optimization}

使用`useRedirectedUrl`属性打开(true)或关闭(false)302重定向。
例如：

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration as Metadata: 
MetadataNode resourceMetadata = new MetadataNode();  
resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                         networkConfiguration); 
 
//Call MediaResource.createFromURL to set the metadata: 
MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
  
//Load the resource 
mediaPlayer.replaceCurrentItem(resource);
```

