---
description: 302重定向优化可最大限度地减少302个重定向响应的数量，从而使您的应用程序可以更有效地进行负载平衡。
title: 禁用或启用302重定向优化
exl-id: b1bdb6d6-b34d-4e0a-8c96-7fd4ce77b5c9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# HTTP 302重定向优化 {#http-302-redirect-optimization}

302重定向优化可最大限度地减少302个重定向响应的数量，从而使您的应用程序可以更有效地进行负载平衡。

如果重定向主清单请求，并在播放器中启用302优化，则从该清单对资产发出的后续请求将使用最终域位置，从而避免额外302响应。

此功能默认处于启用状态，您可以更改此设置。

## 禁用或启用302重定向优化{#disable-or-enable-redirect-optimization}

使用 `useRedirectedUrl` 属性以打开(true)或关闭(false)302重定向。
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
